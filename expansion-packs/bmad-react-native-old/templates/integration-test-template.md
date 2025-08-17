// Integration Test Template for React Native
// Tests complete user workflows and component interactions
// Replace [FeatureName] with your actual feature name

import React from 'react';
import { render, fireEvent, waitFor, within } from '@testing-library/react-native';
import { NavigationContainer } from '@react-navigation/native';
import { [FeatureName]Screen } from '../src/screens/[FeatureName]Screen';
import { [FeatureName]Provider } from '../src/contexts/[FeatureName]Context';

// Mock navigation
const mockNavigation = {
  navigate: jest.fn(),
  goBack: jest.fn(),
  setOptions: jest.fn(),
  canGoBack: jest.fn(() => true),
};

// Mock API calls
jest.mock('../src/services/api', () => ({
  login: jest.fn(),
  fetchUserProfile: jest.fn(),
  updateProfile: jest.fn(),
  logout: jest.fn(),
}));

// Mock async storage
jest.mock('@react-native-async-storage/async-storage', () => ({
  getItem: jest.fn(),
  setItem: jest.fn(),
  removeItem: jest.fn(),
  clear: jest.fn(),
}));

// Mock native modules
jest.mock('react-native', () => ({
  ...jest.requireActual('react-native'),
  Alert: {
    alert: jest.fn(),
  },
  Linking: {
    openURL: jest.fn(),
  },
}));

describe('[FeatureName] Integration Tests', () => {
  // Test setup and cleanup
  beforeEach(() => {
    jest.clearAllMocks();
  });

  afterEach(() => {
    jest.restoreAllMocks();
  });

  // Helper function to render component with all providers
  const renderWithProviders = (component, options = {}) => {
    const { initialState = {}, navigationProps = {} } = options;

    return render(
      <NavigationContainer>
        <[FeatureName]Provider initialState={initialState}>
          {React.cloneElement(component, {
            navigation: { ...mockNavigation, ...navigationProps },
            ...component.props,
          })}
        </[FeatureName]Provider>
      </NavigationContainer>
    );
  };

  describe('Complete User Workflow', () => {
    it('should complete the entire login flow', async () => {
      const mockLogin = require('../src/services/api').login;
      const mockFetchProfile = require('../src/services/api').fetchUserProfile;
      
      mockLogin.mockResolvedValue({
        token: 'fake-token',
        user: { id: 1, email: 'test@example.com' },
      });
      mockFetchProfile.mockResolvedValue({
        id: 1,
        email: 'test@example.com',
        name: 'Test User',
      });

      const { getByTestId, getByText } = renderWithProviders(
        <[FeatureName]Screen />
      );

      // Step 1: Fill login form
      fireEvent.changeText(getByTestId('email-input'), 'test@example.com');
      fireEvent.changeText(getByTestId('password-input'), 'password123');

      // Step 2: Submit form
      fireEvent.press(getByTestId('login-button'));

      // Step 3: Verify loading state
      expect(getByTestId('loading-indicator')).toBeTruthy();

      // Step 4: Wait for successful login
      await waitFor(() => {
        expect(mockLogin).toHaveBeenCalledWith({
          email: 'test@example.com',
          password: 'password123',
        });
      });

      // Step 5: Verify navigation to next screen
      await waitFor(() => {
        expect(mockNavigation.navigate).toHaveBeenCalledWith('Dashboard');
      });

      // Step 6: Verify user profile was fetched
      expect(mockFetchProfile).toHaveBeenCalledWith('fake-token');
    });

    it('should handle login failure gracefully', async () => {
      const mockLogin = require('../src/services/api').login;
      mockLogin.mockRejectedValue(new Error('Invalid credentials'));

      const { getByTestId, getByText } = renderWithProviders(
        <[FeatureName]Screen />
      );

      // Fill form and submit
      fireEvent.changeText(getByTestId('email-input'), 'test@example.com');
      fireEvent.changeText(getByTestId('password-input'), 'wrongpassword');
      fireEvent.press(getByTestId('login-button'));

      // Wait for error message
      await waitFor(() => {
        expect(getByText(/invalid credentials/i)).toBeTruthy();
      });

      // Verify user stays on login screen
      expect(mockNavigation.navigate).not.toHaveBeenCalled();
    });
  });

  describe('Form Validation Integration', () => {
    it('should validate form fields and show errors', async () => {
      const { getByTestId, getByText, queryByText } = renderWithProviders(
        <[FeatureName]Screen />
      );

      // Submit empty form
      fireEvent.press(getByTestId('submit-button'));

      // Check for validation errors
      await waitFor(() => {
        expect(getByText('Email is required')).toBeTruthy();
        expect(getByText('Password is required')).toBeTruthy();
      });

      // Fill email with invalid format
      fireEvent.changeText(getByTestId('email-input'), 'invalid-email');
      fireEvent.press(getByTestId('submit-button'));

      await waitFor(() => {
        expect(getByText('Please enter a valid email')).toBeTruthy();
      });

      // Fix email, check password validation
      fireEvent.changeText(getByTestId('email-input'), 'test@example.com');
      fireEvent.changeText(getByTestId('password-input'), '123'); // Too short
      fireEvent.press(getByTestId('submit-button'));

      await waitFor(() => {
        expect(queryByText('Email is required')).toBeNull();
        expect(getByText('Password must be at least 6 characters')).toBeTruthy();
      });
    });

    it('should clear errors when input becomes valid', async () => {
      const { getByTestId, getByText, queryByText } = renderWithProviders(
        <[FeatureName]Screen />
      );

      // Trigger validation error
      fireEvent.press(getByTestId('submit-button'));
      
      await waitFor(() => {
        expect(getByText('Email is required')).toBeTruthy();
      });

      // Fix the error
      fireEvent.changeText(getByTestId('email-input'), 'test@example.com');

      await waitFor(() => {
        expect(queryByText('Email is required')).toBeNull();
      });
    });
  });

  describe('Navigation Integration', () => {
    it('should navigate between screens correctly', async () => {
      const { getByTestId } = renderWithProviders(<[FeatureName]Screen />);

      // Test navigation to different screens
      fireEvent.press(getByTestId('go-to-profile'));
      expect(mockNavigation.navigate).toHaveBeenCalledWith('Profile');

      fireEvent.press(getByTestId('go-to-settings'));
      expect(mockNavigation.navigate).toHaveBeenCalledWith('Settings');

      fireEvent.press(getByTestId('go-back'));
      expect(mockNavigation.goBack).toHaveBeenCalled();
    });

    it('should pass correct parameters during navigation', async () => {
      const { getByTestId } = renderWithProviders(<[FeatureName]Screen />);

      const itemId = '123';
      fireEvent.press(getByTestId(`item-${itemId}`));

      expect(mockNavigation.navigate).toHaveBeenCalledWith('ItemDetail', {
        itemId,
        fromScreen: '[FeatureName]Screen',
      });
    });
  });

  describe('State Management Integration', () => {
    it('should update global state correctly', async () => {
      const initialState = { user: null, isLoading: false };
      
      const { getByTestId, rerender } = renderWithProviders(
        <[FeatureName]Screen />,
        { initialState }
      );

      // Action that updates state
      fireEvent.press(getByTestId('update-profile'));

      // Wait for state change
      await waitFor(() => {
        expect(getByTestId('loading-indicator')).toBeTruthy();
      });

      // Verify state persisted across re-renders
      rerender(
        <NavigationContainer>
          <[FeatureName]Provider initialState={initialState}>
            <[FeatureName]Screen navigation={mockNavigation} />
          </[FeatureName]Provider>
        </NavigationContainer>
      );

      expect(getByTestId('loading-indicator')).toBeTruthy();
    });

    it('should handle state updates from external actions', async () => {
      const mockAsyncStorage = require('@react-native-async-storage/async-storage');
      mockAsyncStorage.getItem.mockResolvedValue('{"user": {"name": "Cached User"}}');

      const { getByText } = renderWithProviders(<[FeatureName]Screen />);

      await waitFor(() => {
        expect(getByText('Cached User')).toBeTruthy();
      });
    });
  });

  describe('API Integration', () => {
    it('should handle API success responses', async () => {
      const mockApi = require('../src/services/api');
      mockApi.fetchUserProfile.mockResolvedValue({
        id: 1,
        name: 'John Doe',
        email: 'john@example.com',
      });

      const { getByTestId, getByText } = renderWithProviders(
        <[FeatureName]Screen />
      );

      fireEvent.press(getByTestId('refresh-data'));

      await waitFor(() => {
        expect(getByText('John Doe')).toBeTruthy();
        expect(getByText('john@example.com')).toBeTruthy();
      });
    });

    it('should handle API error responses', async () => {
      const mockApi = require('../src/services/api');
      mockApi.fetchUserProfile.mockRejectedValue(
        new Error('Network connection failed')
      );

      const { getByTestId, getByText } = renderWithProviders(
        <[FeatureName]Screen />
      );

      fireEvent.press(getByTestId('refresh-data'));

      await waitFor(() => {
        expect(getByText(/network connection failed/i)).toBeTruthy();
      });
    });

    it('should retry failed API calls', async () => {
      const mockApi = require('../src/services/api');
      mockApi.fetchUserProfile
        .mockRejectedValueOnce(new Error('Temporary error'))
        .mockResolvedValue({ id: 1, name: 'John Doe' });

      const { getByTestId, getByText } = renderWithProviders(
        <[FeatureName]Screen />
      );

      // Initial request fails
      fireEvent.press(getByTestId('refresh-data'));
      
      await waitFor(() => {
        expect(getByText(/temporary error/i)).toBeTruthy();
      });

      // Retry request succeeds
      fireEvent.press(getByTestId('retry-button'));

      await waitFor(() => {
        expect(getByText('John Doe')).toBeTruthy();
      });

      expect(mockApi.fetchUserProfile).toHaveBeenCalledTimes(2);
    });
  });

  describe('Data Persistence Integration', () => {
    it('should save data to async storage', async () => {
      const mockAsyncStorage = require('@react-native-async-storage/async-storage');
      
      const { getByTestId } = renderWithProviders(<[FeatureName]Screen />);

      fireEvent.changeText(getByTestId('settings-input'), 'dark-mode');
      fireEvent.press(getByTestId('save-settings'));

      await waitFor(() => {
        expect(mockAsyncStorage.setItem).toHaveBeenCalledWith(
          'user-settings',
          JSON.stringify({ theme: 'dark-mode' })
        );
      });
    });

    it('should load data from async storage on mount', async () => {
      const mockAsyncStorage = require('@react-native-async-storage/async-storage');
      mockAsyncStorage.getItem.mockResolvedValue(
        JSON.stringify({ theme: 'dark-mode' })
      );

      const { getByTestId } = renderWithProviders(<[FeatureName]Screen />);

      await waitFor(() => {
        expect(mockAsyncStorage.getItem).toHaveBeenCalledWith('user-settings');
        expect(getByTestId('settings-input').props.value).toBe('dark-mode');
      });
    });
  });

  describe('Real-time Updates Integration', () => {
    it('should handle websocket messages', async () => {
      const { getByTestId, getByText } = renderWithProviders(
        <[FeatureName]Screen />
      );

      // Simulate websocket message
      const mockMessage = {
        type: 'USER_UPDATE',
        data: { id: 1, name: 'Updated Name' },
      };

      // Trigger websocket message (this depends on your implementation)
      // You might need to mock your websocket service
      
      await waitFor(() => {
        expect(getByText('Updated Name')).toBeTruthy();
      });
    });
  });

  describe('Error Boundary Integration', () => {
    it('should catch and display component errors', () => {
      const consoleSpy = jest.spyOn(console, 'error').mockImplementation();

      const BrokenComponent = () => {
        throw new Error('Component crashed');
      };

      const { getByText } = renderWithProviders(
        <[FeatureName]Screen>
          <BrokenComponent />
        </[FeatureName]Screen>
      );

      expect(getByText(/something went wrong/i)).toBeTruthy();
      
      consoleSpy.mockRestore();
    });
  });

  describe('Accessibility Integration', () => {
    it('should support screen reader navigation', async () => {
      const { getByLabelText } = renderWithProviders(<[FeatureName]Screen />);

      // Test screen reader can find and interact with elements
      const submitButton = getByLabelText('Submit form');
      expect(submitButton).toBeTruthy();

      fireEvent.press(submitButton);

      await waitFor(() => {
        const successMessage = getByLabelText('Form submitted successfully');
        expect(successMessage).toBeTruthy();
      });
    });

    it('should provide proper focus management', async () => {
      const { getByTestId } = renderWithProviders(<[FeatureName]Screen />);

      const firstInput = getByTestId('first-input');
      const secondInput = getByTestId('second-input');

      // Test tab navigation or focus management
      fireEvent(firstInput, 'onSubmitEditing');

      // Verify focus moved to next input
      // Note: This depends on your focus management implementation
      expect(secondInput.props.focused).toBe(true);
    });
  });

  describe('Performance Integration', () => {
    it('should handle large datasets without performance degradation', async () => {
      const largeDataset = Array.from({ length: 1000 }, (_, i) => ({
        id: i,
        name: `Item ${i}`,
      }));

      const startTime = Date.now();
      
      const { getByTestId } = renderWithProviders(
        <[FeatureName]Screen initialData={largeDataset} />
      );

      await waitFor(() => {
        expect(getByTestId('data-list')).toBeTruthy();
      });

      const renderTime = Date.now() - startTime;
      expect(renderTime).toBeLessThan(1000); // Should render in less than 1 second
    });

    it('should implement proper memoization', () => {
      let renderCount = 0;
      const TrackingComponent = React.memo((props) => {
        renderCount++;
        return <[FeatureName]Screen {...props} />;
      });

      const { rerender } = renderWithProviders(<TrackingComponent prop1="value1" />);

      expect(renderCount).toBe(1);

      // Re-render with same props
      rerender(
        <NavigationContainer>
          <[FeatureName]Provider>
            <TrackingComponent prop1="value1" />
          </[FeatureName]Provider>
        </NavigationContainer>
      );

      // Component should not re-render with same props
      expect(renderCount).toBe(1);

      // Re-render with different props
      rerender(
        <NavigationContainer>
          <[FeatureName]Provider>
            <TrackingComponent prop1="value2" />
          </[FeatureName]Provider>
        </NavigationContainer>
      );

      expect(renderCount).toBe(2);
    });
  });
});

// Helper functions for integration tests
const createMockApiResponse = (data, delay = 0) => {
  return new Promise((resolve) => {
    setTimeout(() => resolve(data), delay);
  });
};

const createMockApiError = (error, delay = 0) => {
  return new Promise((_, reject) => {
    setTimeout(() => reject(error), delay);
  });
};

const simulateNetworkDelay = (ms = 1000) => {
  return new Promise(resolve => setTimeout(resolve, ms));
};

export {
  createMockApiResponse,
  createMockApiError,
  simulateNetworkDelay,
};