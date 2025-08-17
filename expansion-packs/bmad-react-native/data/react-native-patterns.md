# React Native Development Patterns

## Component Architecture Patterns

### Functional Components with Hooks
```typescript
import React, { useState, useEffect, useCallback, useMemo } from 'react';
import { View, Text, FlatList, TouchableOpacity } from 'react-native';

interface User {
  id: string;
  name: string;
  email: string;
}

interface UserListProps {
  users: User[];
  onUserSelect: (user: User) => void;
}

const UserList: React.FC<UserListProps> = ({ users, onUserSelect }) => {
  const [searchTerm, setSearchTerm] = useState('');

  // Memoize filtered users to prevent unnecessary re-calculations
  const filteredUsers = useMemo(() => {
    return users.filter(user => 
      user.name.toLowerCase().includes(searchTerm.toLowerCase())
    );
  }, [users, searchTerm]);

  // Optimize callback to prevent re-renders
  const handleUserPress = useCallback((user: User) => {
    onUserSelect(user);
  }, [onUserSelect]);

  const renderUser = useCallback(({ item }: { item: User }) => (
    <TouchableOpacity onPress={() => handleUserPress(item)}>
      <View style={styles.userItem}>
        <Text>{item.name}</Text>
        <Text>{item.email}</Text>
      </View>
    </TouchableOpacity>
  ), [handleUserPress]);

  const keyExtractor = useCallback((item: User) => item.id, []);

  return (
    <FlatList
      data={filteredUsers}
      renderItem={renderUser}
      keyExtractor={keyExtractor}
      // Performance optimizations
      removeClippedSubviews={true}
      maxToRenderPerBatch={10}
      updateCellsBatchingPeriod={100}
      windowSize={10}
    />
  );
};
```

### Custom Hooks Pattern
```typescript
// Custom hook for API data fetching
import { useState, useEffect } from 'react';

interface UseApiResult<T> {
  data: T | null;
  loading: boolean;
  error: string | null;
  refetch: () => void;
}

function useApi<T>(url: string): UseApiResult<T> {
  const [data, setData] = useState<T | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<string | null>(null);

  const fetchData = useCallback(async () => {
    try {
      setLoading(true);
      setError(null);
      const response = await fetch(url);
      if (!response.ok) throw new Error('Network response was not ok');
      const result = await response.json();
      setData(result);
    } catch (err) {
      setError(err instanceof Error ? err.message : 'An error occurred');
    } finally {
      setLoading(false);
    }
  }, [url]);

  useEffect(() => {
    fetchData();
  }, [fetchData]);

  return { data, loading, error, refetch: fetchData };
}

// Usage
const UserScreen = () => {
  const { data: users, loading, error, refetch } = useApi<User[]>('/api/users');
  
  if (loading) return <LoadingSpinner />;
  if (error) return <ErrorMessage message={error} onRetry={refetch} />;
  
  return <UserList users={users || []} onUserSelect={handleUserSelect} />;
};
```

## State Management Patterns

### Context + Reducer Pattern
```typescript
// Context for global app state
import React, { createContext, useContext, useReducer, ReactNode } from 'react';

interface AppState {
  user: User | null;
  theme: 'light' | 'dark';
  notifications: Notification[];
}

type AppAction = 
  | { type: 'SET_USER'; payload: User | null }
  | { type: 'TOGGLE_THEME' }
  | { type: 'ADD_NOTIFICATION'; payload: Notification }
  | { type: 'REMOVE_NOTIFICATION'; payload: string };

const appReducer = (state: AppState, action: AppAction): AppState => {
  switch (action.type) {
    case 'SET_USER':
      return { ...state, user: action.payload };
    case 'TOGGLE_THEME':
      return { ...state, theme: state.theme === 'light' ? 'dark' : 'light' };
    case 'ADD_NOTIFICATION':
      return { ...state, notifications: [...state.notifications, action.payload] };
    case 'REMOVE_NOTIFICATION':
      return { 
        ...state, 
        notifications: state.notifications.filter(n => n.id !== action.payload) 
      };
    default:
      return state;
  }
};

const AppContext = createContext<{
  state: AppState;
  dispatch: React.Dispatch<AppAction>;
} | null>(null);

export const AppProvider: React.FC<{ children: ReactNode }> = ({ children }) => {
  const [state, dispatch] = useReducer(appReducer, {
    user: null,
    theme: 'light',
    notifications: [],
  });

  return (
    <AppContext.Provider value={{ state, dispatch }}>
      {children}
    </AppContext.Provider>
  );
};

export const useAppContext = () => {
  const context = useContext(AppContext);
  if (!context) {
    throw new Error('useAppContext must be used within AppProvider');
  }
  return context;
};
```

### Zustand Pattern (Lightweight State Management)
```typescript
import { create } from 'zustand';
import { persist, createJSONStorage } from 'zustand/middleware';
import AsyncStorage from '@react-native-async-storage/async-storage';

interface UserStore {
  user: User | null;
  setUser: (user: User | null) => void;
  logout: () => void;
}

export const useUserStore = create<UserStore>()(
  persist(
    (set) => ({
      user: null,
      setUser: (user) => set({ user }),
      logout: () => set({ user: null }),
    }),
    {
      name: 'user-storage',
      storage: createJSONStorage(() => AsyncStorage),
    }
  )
);

// Usage in component
const ProfileScreen = () => {
  const { user, logout } = useUserStore();
  
  return (
    <View>
      <Text>Welcome, {user?.name}</Text>
      <Button title="Logout" onPress={logout} />
    </View>
  );
};
```

## Navigation Patterns

### Type-Safe Navigation
```typescript
// Define navigation types
export type RootStackParamList = {
  Home: undefined;
  Profile: { userId: string };
  Settings: { section?: string };
};

export type BottomTabParamList = {
  HomeTab: undefined;
  SearchTab: undefined;
  ProfileTab: undefined;
};

// Type-safe navigation hook
import { useNavigation } from '@react-navigation/native';
import { StackNavigationProp } from '@react-navigation/stack';

type NavigationProp = StackNavigationProp<RootStackParamList>;

export const useTypedNavigation = () => {
  return useNavigation<NavigationProp>();
};

// Usage
const HomeScreen = () => {
  const navigation = useTypedNavigation();
  
  const goToProfile = (userId: string) => {
    navigation.navigate('Profile', { userId }); // Type-safe!
  };
};
```

### Navigation Service Pattern
```typescript
// navigationService.ts - For navigation outside React components
import { createNavigationContainerRef } from '@react-navigation/native';

export const navigationRef = createNavigationContainerRef<RootStackParamList>();

export function navigate(name: keyof RootStackParamList, params?: any) {
  if (navigationRef.isReady()) {
    navigationRef.navigate(name as any, params);
  }
}

export function goBack() {
  if (navigationRef.isReady()) {
    navigationRef.goBack();
  }
}

// Usage in App.js
<NavigationContainer ref={navigationRef}>
  <AppNavigator />
</NavigationContainer>

// Usage in services or utilities
import { navigate } from './navigationService';

const handlePushNotification = (notification) => {
  navigate('Profile', { userId: notification.userId });
};
```

## Performance Optimization Patterns

### FlatList Optimization
```typescript
const OptimizedList: React.FC<{ data: Item[] }> = ({ data }) => {
  const renderItem = useCallback(({ item, index }: { item: Item; index: number }) => (
    <MemoizedListItem item={item} index={index} />
  ), []);

  const keyExtractor = useCallback((item: Item) => item.id, []);

  const getItemLayout = useCallback((data: any, index: number) => ({
    length: ITEM_HEIGHT,
    offset: ITEM_HEIGHT * index,
    index,
  }), []);

  return (
    <FlatList
      data={data}
      renderItem={renderItem}
      keyExtractor={keyExtractor}
      getItemLayout={getItemLayout} // If items have fixed height
      removeClippedSubviews={true}
      maxToRenderPerBatch={10}
      updateCellsBatchingPeriod={100}
      windowSize={10}
      initialNumToRender={10}
    />
  );
};

const MemoizedListItem = React.memo<{ item: Item; index: number }>(
  ({ item, index }) => (
    <View style={styles.listItem}>
      <Text>{item.title}</Text>
    </View>
  ),
  (prevProps, nextProps) => {
    // Custom comparison for when to re-render
    return prevProps.item.id === nextProps.item.id;
  }
);
```

### Image Optimization Pattern
```typescript
import FastImage from 'react-native-fast-image';

const OptimizedImage: React.FC<{
  uri: string;
  style?: any;
  placeholder?: string;
}> = ({ uri, style, placeholder }) => {
  return (
    <FastImage
      style={style}
      source={{
        uri,
        priority: FastImage.priority.normal,
        cache: FastImage.cacheControl.immutable,
      }}
      resizeMode={FastImage.resizeMode.cover}
      fallback={placeholder && <Image source={{ uri: placeholder }} style={style} />}
    />
  );
};
```

## Platform-Specific Patterns

### Platform-Specific Components
```typescript
import { Platform } from 'react-native';

// Platform-specific components
const PlatformButton: React.FC<ButtonProps> = (props) => {
  if (Platform.OS === 'ios') {
    return <IOSButton {...props} />;
  } else {
    return <AndroidButton {...props} />;
  }
};

// Platform-specific styles
const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: Platform.OS === 'ios' ? 20 : 0,
    ...Platform.select({
      ios: {
        shadowColor: '#000',
        shadowOffset: { width: 0, height: 2 },
        shadowOpacity: 0.1,
        shadowRadius: 4,
      },
      android: {
        elevation: 4,
      },
    }),
  },
});

// Platform-specific values
const HEADER_HEIGHT = Platform.select({
  ios: 64,
  android: 56,
  default: 64,
});
```

### Safe Area Handling
```typescript
import { SafeAreaProvider, SafeAreaView } from 'react-native-safe-area-context';

// App-level setup
const App = () => (
  <SafeAreaProvider>
    <AppContent />
  </SafeAreaProvider>
);

// Screen-level usage
const ScreenComponent = () => (
  <SafeAreaView style={{ flex: 1 }} edges={['top']}>
    <Content />
  </SafeAreaView>
);
```

## Error Handling Patterns

### Error Boundary Pattern
```typescript
import React, { Component, ErrorInfo, ReactNode } from 'react';

interface Props {
  children: ReactNode;
  fallback?: ReactNode;
}

interface State {
  hasError: boolean;
  error?: Error;
}

class ErrorBoundary extends Component<Props, State> {
  constructor(props: Props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error: Error): State {
    return { hasError: true, error };
  }

  componentDidCatch(error: Error, errorInfo: ErrorInfo) {
    console.error('Error caught by boundary:', error, errorInfo);
    // Log to crash reporting service
    crashlytics().recordError(error);
  }

  render() {
    if (this.state.hasError) {
      return this.props.fallback || <ErrorFallback error={this.state.error} />;
    }

    return this.props.children;
  }
}

// Usage
<ErrorBoundary fallback={<CustomErrorScreen />}>
  <App />
</ErrorBoundary>
```

### API Error Handling Pattern
```typescript
interface ApiResponse<T> {
  data?: T;
  error?: string;
  success: boolean;
}

async function apiRequest<T>(url: string, options?: RequestInit): Promise<ApiResponse<T>> {
  try {
    const response = await fetch(url, {
      ...options,
      headers: {
        'Content-Type': 'application/json',
        ...options?.headers,
      },
    });

    if (!response.ok) {
      const errorData = await response.json().catch(() => null);
      return {
        success: false,
        error: errorData?.message || `HTTP ${response.status}: ${response.statusText}`,
      };
    }

    const data = await response.json();
    return { success: true, data };
  } catch (error) {
    return {
      success: false,
      error: error instanceof Error ? error.message : 'Network error occurred',
    };
  }
}

// Usage
const { data, error, success } = await apiRequest<User[]>('/api/users');
if (success && data) {
  setUsers(data);
} else {
  showError(error || 'Unknown error');
}
```

## Testing Patterns

### Component Testing with React Native Testing Library
```typescript
import React from 'react';
import { render, fireEvent, waitFor } from '@testing-library/react-native';
import { UserList } from '../UserList';

const mockUsers = [
  { id: '1', name: 'John Doe', email: 'john@example.com' },
  { id: '2', name: 'Jane Smith', email: 'jane@example.com' },
];

describe('UserList', () => {
  const mockOnUserSelect = jest.fn();

  beforeEach(() => {
    mockOnUserSelect.mockClear();
  });

  it('renders user list correctly', () => {
    const { getByText } = render(
      <UserList users={mockUsers} onUserSelect={mockOnUserSelect} />
    );

    expect(getByText('John Doe')).toBeTruthy();
    expect(getByText('jane@example.com')).toBeTruthy();
  });

  it('calls onUserSelect when user is pressed', () => {
    const { getByText } = render(
      <UserList users={mockUsers} onUserSelect={mockOnUserSelect} />
    );

    fireEvent.press(getByText('John Doe'));
    expect(mockOnUserSelect).toHaveBeenCalledWith(mockUsers[0]);
  });
});
```

### Hook Testing Pattern
```typescript
import { renderHook, act } from '@testing-library/react-hooks';
import { useApi } from '../useApi';

// Mock fetch
global.fetch = jest.fn();

describe('useApi', () => {
  beforeEach(() => {
    (fetch as jest.Mock).mockClear();
  });

  it('should fetch data successfully', async () => {
    const mockData = { id: 1, name: 'Test' };
    (fetch as jest.Mock).mockResolvedValueOnce({
      ok: true,
      json: async () => mockData,
    });

    const { result, waitForNextUpdate } = renderHook(() => useApi('/test'));

    expect(result.current.loading).toBe(true);
    await waitForNextUpdate();

    expect(result.current.loading).toBe(false);
    expect(result.current.data).toEqual(mockData);
    expect(result.current.error).toBe(null);
  });
});
```

## Animation Patterns

### Reanimated 3 Patterns
```typescript
import Animated, {
  useSharedValue,
  useAnimatedStyle,
  withTiming,
  withSpring,
  runOnJS,
} from 'react-native-reanimated';

const AnimatedButton: React.FC<{ onPress: () => void }> = ({ onPress }) => {
  const scale = useSharedValue(1);
  const opacity = useSharedValue(1);

  const animatedStyle = useAnimatedStyle(() => ({
    transform: [{ scale: scale.value }],
    opacity: opacity.value,
  }));

  const handlePressIn = () => {
    scale.value = withSpring(0.95);
    opacity.value = withTiming(0.8);
  };

  const handlePressOut = () => {
    scale.value = withSpring(1);
    opacity.value = withTiming(1, {}, (finished) => {
      if (finished) {
        runOnJS(onPress)();
      }
    });
  };

  return (
    <Animated.View style={animatedStyle}>
      <TouchableWithoutFeedback
        onPressIn={handlePressIn}
        onPressOut={handlePressOut}
      >
        <View style={styles.button}>
          <Text>Press me</Text>
        </View>
      </TouchableWithoutFeedback>
    </Animated.View>
  );
};
```

These patterns provide a solid foundation for React Native development, covering component architecture, state management, navigation, performance optimization, platform-specific code, error handling, testing, and animations.