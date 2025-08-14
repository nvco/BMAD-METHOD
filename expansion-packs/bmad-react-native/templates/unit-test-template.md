// Unit Test Template for React Native Components
// Replace [ComponentName] with your actual component name
// This template uses Jest + React Native Testing Library

import React from 'react';
import { render, fireEvent, waitFor, screen } from '@testing-library/react-native';
import { [ComponentName] } from '../src/components/[ComponentName]';

// Mock dependencies if needed
jest.mock('../src/services/api', () => ({
  fetchData: jest.fn(),
}));

// Mock React Native modules if needed
jest.mock('react-native', () => ({
  ...jest.requireActual('react-native'),
  Platform: {
    OS: 'ios',
    select: jest.fn((obj) => obj.ios),
  },
  Dimensions: {
    get: jest.fn(() => ({ width: 375, height: 812 })),
  },
}));

describe('[ComponentName]', () => {
  // Reset mocks before each test
  beforeEach(() => {
    jest.clearAllMocks();
  });

  // Clean up after tests
  afterEach(() => {
    jest.restoreAllMocks();
  });

  describe('Rendering', () => {
    it('should render correctly with default props', () => {
      const { getByTestId } = render(<[ComponentName] />);
      
      // Assert component renders
      expect(getByTestId('[component-test-id]')).toBeTruthy();
    });

    it('should render with custom props', () => {
      const mockProps = {
        title: 'Test Title',
        onPress: jest.fn(),
        disabled: false,
      };

      const { getByText } = render(<[ComponentName] {...mockProps} />);
      
      expect(getByText('Test Title')).toBeTruthy();
    });

    it('should render different states correctly', () => {
      // Test loading state
      const { rerender, getByTestId, queryByTestId } = render(
        <[ComponentName] loading={true} />
      );
      expect(getByTestId('loading-indicator')).toBeTruthy();

      // Test error state
      rerender(<[ComponentName] error="Something went wrong" />);
      expect(getByText('Something went wrong')).toBeTruthy();

      // Test success state
      rerender(<[ComponentName] data={mockData} />);
      expect(queryByTestId('loading-indicator')).toBeNull();
    });
  });

  describe('User Interactions', () => {
    it('should handle press events', async () => {
      const mockOnPress = jest.fn();
      const { getByTestId } = render(
        <[ComponentName] onPress={mockOnPress} />
      );

      fireEvent.press(getByTestId('[pressable-element]'));
      
      expect(mockOnPress).toHaveBeenCalledTimes(1);
    });

    it('should handle text input changes', async () => {
      const mockOnChange = jest.fn();
      const { getByTestId } = render(
        <[ComponentName] onTextChange={mockOnChange} />
      );

      fireEvent.changeText(getByTestId('text-input'), 'New text');
      
      expect(mockOnChange).toHaveBeenCalledWith('New text');
    });

    it('should handle form submission', async () => {
      const mockOnSubmit = jest.fn();
      const { getByTestId } = render(
        <[ComponentName] onSubmit={mockOnSubmit} />
      );

      // Fill form fields
      fireEvent.changeText(getByTestId('email-input'), 'test@example.com');
      fireEvent.changeText(getByTestId('password-input'), 'password123');
      
      // Submit form
      fireEvent.press(getByTestId('submit-button'));
      
      await waitFor(() => {
        expect(mockOnSubmit).toHaveBeenCalledWith({
          email: 'test@example.com',
          password: 'password123',
        });
      });
    });
  });

  describe('API Integration', () => {
    it('should fetch data on mount', async () => {
      const mockFetchData = require('../src/services/api').fetchData;
      mockFetchData.mockResolvedValue({ data: 'test data' });

      render(<[ComponentName] />);

      await waitFor(() => {
        expect(mockFetchData).toHaveBeenCalledTimes(1);
      });
    });

    it('should handle API errors gracefully', async () => {
      const mockFetchData = require('../src/services/api').fetchData;
      mockFetchData.mockRejectedValue(new Error('Network error'));

      const { getByText } = render(<[ComponentName] />);

      await waitFor(() => {
        expect(getByText(/error/i)).toBeTruthy();
      });
    });

    it('should retry failed requests', async () => {
      const mockFetchData = require('../src/services/api').fetchData;
      mockFetchData
        .mockRejectedValueOnce(new Error('Network error'))
        .mockResolvedValue({ data: 'success' });

      const { getByTestId } = render(<[ComponentName] />);

      // Wait for initial error
      await waitFor(() => {
        expect(getByTestId('error-message')).toBeTruthy();
      });

      // Trigger retry
      fireEvent.press(getByTestId('retry-button'));

      await waitFor(() => {
        expect(mockFetchData).toHaveBeenCalledTimes(2);
        expect(getByTestId('success-content')).toBeTruthy();
      });
    });
  });

  describe('State Management', () => {
    it('should update state correctly', async () => {
      const { getByTestId } = render(<[ComponentName] />);

      // Initial state
      expect(getByTestId('counter')).toHaveTextContent('0');

      // Update state
      fireEvent.press(getByTestId('increment-button'));

      await waitFor(() => {
        expect(getByTestId('counter')).toHaveTextContent('1');
      });
    });

    it('should handle multiple state updates', async () => {
      const { getByTestId } = render(<[ComponentName] initialValue={5} />);

      fireEvent.press(getByTestId('increment-button'));
      fireEvent.press(getByTestId('increment-button'));
      fireEvent.press(getByTestId('decrement-button'));

      await waitFor(() => {
        expect(getByTestId('counter')).toHaveTextContent('6');
      });
    });
  });

  describe('Conditional Rendering', () => {
    it('should show/hide elements based on props', () => {
      const { rerender, queryByTestId } = render(
        <[ComponentName] showOptionalContent={false} />
      );

      expect(queryByTestId('optional-content')).toBeNull();

      rerender(<[ComponentName] showOptionalContent={true} />);

      expect(queryByTestId('optional-content')).toBeTruthy();
    });

    it('should render different content for different user types', () => {
      const { rerender, getByText, queryByText } = render(
        <[ComponentName] userType="guest" />
      );

      expect(getByText('Welcome, Guest!')).toBeTruthy();
      expect(queryByText('Dashboard')).toBeNull();

      rerender(<[ComponentName] userType="admin" />);

      expect(getByText('Admin Dashboard')).toBeTruthy();
      expect(queryByText('Welcome, Guest!')).toBeNull();
    });
  });

  describe('Accessibility', () => {
    it('should have proper accessibility labels', () => {
      const { getByLabelText } = render(<[ComponentName] />);
      
      expect(getByLabelText('Main content')).toBeTruthy();
      expect(getByLabelText('Submit button')).toBeTruthy();
    });

    it('should have proper accessibility roles', () => {
      const { getByRole } = render(<[ComponentName] />);
      
      expect(getByRole('button')).toBeTruthy();
      expect(getByRole('textbox')).toBeTruthy();
    });

    it('should support screen readers', () => {
      const { getByTestId } = render(<[ComponentName] />);
      
      const element = getByTestId('main-content');
      expect(element.props.accessible).toBe(true);
      expect(element.props.accessibilityLabel).toBeTruthy();
    });
  });

  describe('Performance', () => {
    it('should not re-render unnecessarily', () => {
      const mockRender = jest.fn();
      const ComponentWithTracking = (props) => {
        mockRender();
        return <[ComponentName] {...props} />;
      };

      const { rerender } = render(<ComponentWithTracking prop1="value1" />);
      
      // Initial render
      expect(mockRender).toHaveBeenCalledTimes(1);

      // Re-render with same props shouldn't cause re-render (if component is memoized)
      rerender(<ComponentWithTracking prop1="value1" />);
      
      // This depends on whether your component is wrapped with React.memo
      // expect(mockRender).toHaveBeenCalledTimes(1);
    });

    it('should handle large datasets efficiently', () => {
      const largeDataset = Array.from({ length: 1000 }, (_, i) => ({
        id: i,
        name: `Item ${i}`,
      }));

      const startTime = Date.now();
      render(<[ComponentName] data={largeDataset} />);
      const renderTime = Date.now() - startTime;

      // Should render large datasets in reasonable time (< 100ms)
      expect(renderTime).toBeLessThan(100);
    });
  });

  describe('Error Boundaries', () => {
    it('should catch and handle errors gracefully', () => {
      // Mock console.error to avoid noise in tests
      const consoleSpy = jest.spyOn(console, 'error').mockImplementation();

      const ThrowError = () => {
        throw new Error('Test error');
      };

      // If your component has error boundary
      const { getByText } = render(
        <[ComponentName]>
          <ThrowError />
        </[ComponentName]>
      );

      expect(getByText(/something went wrong/i)).toBeTruthy();
      
      consoleSpy.mockRestore();
    });
  });
});

// Additional test utilities and helpers

// Helper function to create mock data
const createMockData = (count = 10) => {
  return Array.from({ length: count }, (_, i) => ({
    id: i + 1,
    name: `Test Item ${i + 1}`,
    description: `Description for item ${i + 1}`,
    createdAt: new Date().toISOString(),
  }));
};

// Helper function to simulate async operations
const waitForAsync = () => new Promise(resolve => setTimeout(resolve, 0));

// Helper function to create component with providers
const renderWithProviders = (component, { initialState = {} } = {}) => {
  const AllTheProviders = ({ children }) => {
    return (
      <TestProvider initialState={initialState}>
        {children}
      </TestProvider>
    );
  };

  return render(component, { wrapper: AllTheProviders });
};

// Export helpers if needed in other test files
export { createMockData, waitForAsync, renderWithProviders };