// E2E Test Template for React Native using Detox
// Tests complete user journeys across the entire app
// Replace [AppName] and [FeatureName] with your actual names

import { device, element, by, expect, waitFor } from 'detox';

describe('[AppName] E2E Tests', () => {
  beforeAll(async () => {
    await device.launchApp();
  });

  beforeEach(async () => {
    await device.reloadReactNative();
  });

  afterAll(async () => {
    await device.terminateApp();
  });

  describe('App Launch and Navigation', () => {
    it('should launch app and show welcome screen', async () => {
      await waitFor(element(by.id('welcome-screen')))
        .toBeVisible()
        .withTimeout(10000);
      
      await expect(element(by.text('Welcome to [AppName]'))).toBeVisible();
    });

    it('should navigate through main screens', async () => {
      // Navigate to Home tab
      await element(by.id('home-tab')).tap();
      await waitFor(element(by.id('home-screen'))).toBeVisible();

      // Navigate to Profile tab  
      await element(by.id('profile-tab')).tap();
      await waitFor(element(by.id('profile-screen'))).toBeVisible();

      // Navigate to Settings tab
      await element(by.id('settings-tab')).tap();
      await waitFor(element(by.id('settings-screen'))).toBeVisible();
    });

    it('should handle back navigation correctly', async () => {
      // Navigate to detail screen
      await element(by.id('item-list')).tap();
      await element(by.id('first-item')).tap();
      
      await waitFor(element(by.id('item-detail-screen'))).toBeVisible();

      // Go back using back button
      await element(by.id('back-button')).tap();
      
      await waitFor(element(by.id('item-list-screen'))).toBeVisible();
    });
  });

  describe('User Authentication Flow', () => {
    it('should complete full login flow', async () => {
      // Navigate to login screen
      await element(by.id('login-button')).tap();
      await waitFor(element(by.id('login-screen'))).toBeVisible();

      // Fill login form
      await element(by.id('email-input')).typeText('test@example.com');
      await element(by.id('password-input')).typeText('password123');
      
      // Dismiss keyboard if needed
      if (device.getPlatform() === 'ios') {
        await element(by.id('password-input')).tapReturnKey();
      }

      // Submit login
      await element(by.id('submit-login')).tap();

      // Wait for login to complete and navigate to main screen
      await waitFor(element(by.id('main-screen')))
        .toBeVisible()
        .withTimeout(5000);

      // Verify user is logged in
      await expect(element(by.text('Welcome back!'))).toBeVisible();
    });

    it('should handle login errors', async () => {
      await element(by.id('login-button')).tap();
      
      // Enter invalid credentials
      await element(by.id('email-input')).typeText('invalid@example.com');
      await element(by.id('password-input')).typeText('wrongpassword');
      
      await element(by.id('submit-login')).tap();

      // Wait for error message
      await waitFor(element(by.text('Invalid credentials')))
        .toBeVisible()
        .withTimeout(3000);

      // Verify user stays on login screen
      await expect(element(by.id('login-screen'))).toBeVisible();
    });

    it('should complete logout flow', async () => {
      // First login (assuming previous test or setup)
      await element(by.id('profile-tab')).tap();
      await element(by.id('logout-button')).tap();

      // Confirm logout if there's a confirmation dialog
      if (device.getPlatform() === 'ios') {
        await element(by.text('Logout')).tap();
      } else {
        await element(by.text('LOGOUT')).tap();
      }

      // Verify returned to welcome/login screen
      await waitFor(element(by.id('welcome-screen')))
        .toBeVisible()
        .withTimeout(3000);
    });
  });

  describe('Form Interactions', () => {
    it('should fill and submit a complex form', async () => {
      // Navigate to form screen
      await element(by.id('create-item-button')).tap();
      await waitFor(element(by.id('form-screen'))).toBeVisible();

      // Fill text inputs
      await element(by.id('title-input')).typeText('Test Item Title');
      await element(by.id('description-input')).typeText('This is a test description for the item.');

      // Interact with picker/dropdown
      await element(by.id('category-picker')).tap();
      await element(by.text('Electronics')).tap();

      // Toggle switches
      await element(by.id('featured-toggle')).tap();
      await element(by.id('available-toggle')).tap();

      // Select date (if date picker is present)
      await element(by.id('date-picker')).tap();
      // Handle date picker interaction based on platform
      if (device.getPlatform() === 'ios') {
        await element(by.id('confirm-date')).tap();
      }

      // Submit form
      await element(by.id('submit-form')).tap();

      // Verify success message or navigation
      await waitFor(element(by.text('Item created successfully')))
        .toBeVisible()
        .withTimeout(5000);
    });

    it('should validate form fields', async () => {
      await element(by.id('create-item-button')).tap();
      
      // Try to submit empty form
      await element(by.id('submit-form')).tap();

      // Check for validation errors
      await expect(element(by.text('Title is required'))).toBeVisible();
      await expect(element(by.text('Description is required'))).toBeVisible();

      // Fill one field and check partial validation
      await element(by.id('title-input')).typeText('Title Only');
      await element(by.id('submit-form')).tap();

      // Title error should be gone, description error should remain
      await expect(element(by.text('Title is required'))).not.toBeVisible();
      await expect(element(by.text('Description is required'))).toBeVisible();
    });
  });

  describe('List Operations', () => {
    it('should scroll through long lists', async () => {
      await element(by.id('items-list-tab')).tap();
      
      // Wait for list to load
      await waitFor(element(by.id('items-list'))).toBeVisible();

      // Scroll to bottom
      await element(by.id('items-list')).scrollTo('bottom');
      
      // Verify bottom items are visible
      await expect(element(by.id('load-more-button'))).toBeVisible();

      // Scroll back to top
      await element(by.id('items-list')).scrollTo('top');
      
      // Verify top items are visible
      await expect(element(by.id('first-item'))).toBeVisible();
    });

    it('should handle pull-to-refresh', async () => {
      await element(by.id('items-list')).swipe('down', 'fast', 0.8);
      
      // Wait for refresh to complete
      await waitFor(element(by.id('refresh-indicator')))
        .not.toBeVisible()
        .withTimeout(5000);

      // Verify list was refreshed (check for updated timestamp or new items)
      await expect(element(by.id('last-updated-indicator'))).toBeVisible();
    });

    it('should search and filter items', async () => {
      // Open search
      await element(by.id('search-button')).tap();
      await waitFor(element(by.id('search-input'))).toBeVisible();

      // Type search query
      await element(by.id('search-input')).typeText('electronics');
      
      // Wait for filtered results
      await waitFor(element(by.id('filtered-results')))
        .toBeVisible()
        .withTimeout(3000);

      // Verify search results
      await expect(element(by.text('Electronics Item 1'))).toBeVisible();
      await expect(element(by.text('Books Item 1'))).not.toBeVisible();

      // Clear search
      await element(by.id('clear-search')).tap();
      
      // Verify all items are visible again
      await expect(element(by.text('Books Item 1'))).toBeVisible();
    });
  });

  describe('Device-Specific Features', () => {
    it('should handle device orientation changes', async () => {
      await device.setOrientation('landscape');
      
      // Verify layout adapts to landscape
      await expect(element(by.id('main-content'))).toBeVisible();
      
      // Test functionality in landscape mode
      await element(by.id('test-button')).tap();
      await expect(element(by.id('test-result'))).toBeVisible();

      // Rotate back to portrait
      await device.setOrientation('portrait');
      
      // Verify layout works in portrait
      await expect(element(by.id('main-content'))).toBeVisible();
    });

    it('should handle push notifications', async () => {
      // Send mock push notification
      await device.sendUserNotification({
        trigger: {
          type: 'push',
        },
        title: 'Test Notification',
        subtitle: 'Test Subtitle',
        body: 'This is a test notification body',
        badge: 1,
        payload: {
          key1: 'value1',
          key2: 'value2',
        },
      });

      // Verify app handles notification correctly
      await waitFor(element(by.text('New notification received')))
        .toBeVisible()
        .withTimeout(3000);
    });

    it('should handle app backgrounding and foregrounding', async () => {
      // Send app to background
      await device.sendToHome();
      
      // Bring app back to foreground
      await device.launchApp({ newInstance: false });
      
      // Verify app state is maintained
      await expect(element(by.id('main-screen'))).toBeVisible();
      
      // Verify any background sync completed
      await waitFor(element(by.id('sync-complete-indicator')))
        .toBeVisible()
        .withTimeout(3000);
    });
  });

  describe('Error Handling and Recovery', () => {
    it('should handle network connectivity issues', async () => {
      // Disable network connectivity
      await device.setURLBlacklist(['*']);
      
      // Try to perform network operation
      await element(by.id('refresh-data-button')).tap();
      
      // Verify offline message is shown
      await waitFor(element(by.text('No internet connection')))
        .toBeVisible()
        .withTimeout(3000);

      // Re-enable network
      await device.setURLBlacklist([]);
      
      // Retry operation
      await element(by.id('retry-button')).tap();
      
      // Verify data loads successfully
      await waitFor(element(by.id('data-loaded-indicator')))
        .toBeVisible()
        .withTimeout(5000);
    });

    it('should recover from app crashes', async () => {
      // Simulate app crash scenario (this depends on your implementation)
      await element(by.id('trigger-crash-button')).tap();
      
      // App should restart
      await device.launchApp({ newInstance: true });
      
      // Verify app starts up normally
      await waitFor(element(by.id('welcome-screen')))
        .toBeVisible()
        .withTimeout(10000);
      
      // Verify crash was reported (check analytics or logs)
      await expect(element(by.id('main-content'))).toBeVisible();
    });
  });

  describe('Deep Linking', () => {
    it('should handle deep links correctly', async () => {
      // Open deep link
      await device.openURL({ url: 'myapp://item/123' });
      
      // Verify app opens to correct screen
      await waitFor(element(by.id('item-detail-screen')))
        .toBeVisible()
        .withTimeout(5000);
      
      // Verify correct item is displayed
      await expect(element(by.id('item-123'))).toBeVisible();
    });

    it('should handle invalid deep links', async () => {
      await device.openURL({ url: 'myapp://invalid/path' });
      
      // Should fallback to home screen or show error
      await waitFor(element(by.id('home-screen')))
        .toBeVisible()
        .withTimeout(5000);
    });
  });

  describe('Performance and User Experience', () => {
    it('should load screens quickly', async () => {
      const startTime = Date.now();
      
      await element(by.id('heavy-screen-button')).tap();
      await waitFor(element(by.id('heavy-screen'))).toBeVisible();
      
      const loadTime = Date.now() - startTime;
      
      // Screen should load in reasonable time (< 3 seconds)
      expect(loadTime).toBeLessThan(3000);
    });

    it('should maintain smooth animations', async () => {
      // Test smooth scrolling
      await element(by.id('items-list')).scroll(300, 'down');
      
      // Test smooth navigation transitions
      await element(by.id('animated-transition-button')).tap();
      await waitFor(element(by.id('destination-screen'))).toBeVisible();
      
      // Verify no janky animations (this is more of a visual check)
      await expect(element(by.id('destination-screen'))).toBeVisible();
    });

    it('should handle memory pressure gracefully', async () => {
      // Perform memory-intensive operations
      for (let i = 0; i < 10; i++) {
        await element(by.id('load-large-image')).tap();
        await waitFor(element(by.id(`image-${i}`))).toBeVisible();
      }
      
      // Verify app remains responsive
      await element(by.id('test-responsiveness')).tap();
      await expect(element(by.id('response-indicator'))).toBeVisible();
    });
  });

  describe('Accessibility', () => {
    it('should support screen reader navigation', async () => {
      // Enable accessibility on device
      await device.setAccessibility(true);
      
      // Navigate using accessibility features
      await element(by.id('main-button')).tap();
      
      // Verify accessibility labels are present
      await expect(element(by.label('Main navigation button'))).toBeVisible();
      
      await device.setAccessibility(false);
    });

    it('should support voice control', async () => {
      // Test voice control commands (iOS specific)
      if (device.getPlatform() === 'ios') {
        await element(by.label('Submit form')).tap();
        await expect(element(by.id('form-submitted'))).toBeVisible();
      }
    });
  });
});

// Platform-specific test suites
describe('iOS Specific Features', () => {
  beforeAll(async () => {
    if (device.getPlatform() !== 'ios') {
      return; // Skip iOS tests on Android
    }
  });

  it('should handle iOS-specific gestures', async () => {
    if (device.getPlatform() !== 'ios') return;

    // Test iOS swipe gestures
    await element(by.id('swipeable-item')).swipe('left', 'fast');
    await expect(element(by.id('delete-button'))).toBeVisible();

    await element(by.id('swipeable-item')).swipe('right', 'fast');
    await expect(element(by.id('archive-button'))).toBeVisible();
  });

  it('should handle iOS alerts and action sheets', async () => {
    if (device.getPlatform() !== 'ios') return;

    await element(by.id('show-action-sheet')).tap();
    
    // Handle iOS action sheet
    await expect(element(by.text('Choose an option'))).toBeVisible();
    await element(by.text('Option 1')).tap();
    
    await expect(element(by.text('Option 1 selected'))).toBeVisible();
  });
});

describe('Android Specific Features', () => {
  beforeAll(async () => {
    if (device.getPlatform() !== 'android') {
      return; // Skip Android tests on iOS
    }
  });

  it('should handle Android back button', async () => {
    if (device.getPlatform() !== 'android') return;

    // Navigate to detail screen
    await element(by.id('detail-button')).tap();
    await waitFor(element(by.id('detail-screen'))).toBeVisible();

    // Use Android back button
    await device.pressBack();
    
    // Verify returned to previous screen
    await waitFor(element(by.id('main-screen'))).toBeVisible();
  });

  it('should handle Android permissions', async () => {
    if (device.getPlatform() !== 'android') return;

    // Trigger permission request
    await element(by.id('request-camera-permission')).tap();
    
    // Handle system permission dialog
    await element(by.text('ALLOW')).tap();
    
    // Verify permission granted
    await expect(element(by.text('Camera permission granted'))).toBeVisible();
  });
});

// Helper functions for E2E tests
const waitForElementToLoad = async (elementId, timeout = 10000) => {
  await waitFor(element(by.id(elementId)))
    .toBeVisible()
    .withTimeout(timeout);
};

const fillForm = async (formData) => {
  for (const [fieldId, value] of Object.entries(formData)) {
    await element(by.id(fieldId)).typeText(value);
  }
};

const scrollToElement = async (listId, elementId) => {
  await waitFor(element(by.id(elementId)))
    .toBeVisible()
    .whileElement(by.id(listId))
    .scroll(300, 'down');
};

export {
  waitForElementToLoad,
  fillForm,
  scrollToElement,
};