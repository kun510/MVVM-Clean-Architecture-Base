# MVVM-Clean-Architecture-Base

## Directory Tree Structure

This project implements **MVVM (Model-View-ViewModel) pattern** within a **Clean Architecture** framework for an Android News Application built with Jetpack Compose.

### Complete Directory Structure

```
app/src/main/java/com/loc/newsapp/
├── data/                                  # DATA LAYER
│   ├── local/                            # Local Data Sources
│   │   ├── NewsDao.kt                    # Room Database DAO
│   │   ├── NewsDatabase.kt               # Room Database Configuration
│   │   └── NewsTypeConvertor.kt          # Type Converters for Room
│   ├── manger/                           # Data Managers Implementation
│   │   └── LocalUserMangerImpl.kt        # User preferences implementation
│   ├── remote/                           # Remote Data Sources
│   │   ├── dto/                          # Data Transfer Objects
│   │   │   └── NewsResponse.kt           # API Response Models
│   │   ├── NewsApi.kt                    # Retrofit API Interface
│   │   ├── NewsPagingSource.kt           # Paging Source for News
│   │   └── SearchNewsPagingSource.kt     # Paging Source for Search
│   └── repository/                       # Repository Implementations
│       └── NewsRepositoryImpl.kt         # Repository Pattern Implementation
├── di/                                   # DEPENDENCY INJECTION LAYER
│   ├── AppModule.kt                      # Application-level Dependencies
│   ├── MangerModule.kt                   # Manager Dependencies
│   └── RepositoryModule.kt               # Repository Dependencies
├── domain/                               # DOMAIN LAYER (Business Logic)
│   ├── manger/                           # Domain Managers (Interfaces)
│   │   └── LocalUserManger.kt            # User preferences interface
│   ├── model/                            # Domain Models
│   │   ├── Article.kt                    # Core Article Entity
│   │   └── Source.kt                     # News Source Entity
│   ├── repository/                       # Repository Interfaces
│   │   └── NewsRepository.kt             # Repository Contract
│   └── usecases/                         # Business Use Cases
│       ├── app_entry/                    # App Entry Use Cases
│       │   ├── ReadAppEntry.kt           # Read app entry status
│       │   └── SaveAppEntry.kt           # Save app entry status
│       └── news/                         # News-related Use Cases
│           ├── DeleteArticle.kt          # Delete saved article
│           ├── GetNews.kt                # Get news articles
│           ├── GetSavedArticle.kt        # Get single saved article
│           ├── GetSavedArticles.kt       # Get all saved articles
│           ├── SearchNews.kt             # Search news articles
│           └── UpsertArticle.kt          # Insert/Update article
├── presentation/                         # PRESENTATION LAYER (MVVM)
│   ├── bookmark/                         # Bookmark Feature (MVVM)
│   │   ├── BookmarkScreen.kt             # VIEW - Compose UI
│   │   ├── BookmarkState.kt              # MODEL - UI State
│   │   └── BookmarkViewModel.kt          # VIEWMODEL - Business Logic
│   ├── common/                           # Shared UI Components
│   │   ├── ArticleShimmerEffect.kt       # Loading animations
│   │   ├── ArticlesList.kt               # Reusable article list
│   │   ├── EmptyScreen.kt                # Empty state screen
│   │   ├── NewsButton.kt                 # Custom button component
│   │   └── SearchBar.kt                  # Search input component
│   ├── details/                          # Article Details Feature (MVVM)
│   │   ├── components/                   # Feature-specific components
│   │   │   └── DetailsTopBar.kt          # Details screen top bar
│   │   ├── DetailsEvent.kt               # User events/actions
│   │   ├── DetailsScreen.kt              # VIEW - Compose UI
│   │   └── DetailsViewModel.kt           # VIEWMODEL - Business Logic
│   ├── home/                             # Home Feature (MVVM)
│   │   ├── components/                   # Feature-specific components
│   │   │   └── ArticleCard.kt            # Article display card
│   │   ├── HomeScreen.kt                 # VIEW - Compose UI
│   │   ├── HomeState.kt                  # MODEL - UI State
│   │   └── HomeViewModel.kt              # VIEWMODEL - Business Logic
│   ├── mainActivity/                     # Main Activity (MVVM)
│   │   ├── MainActivity.kt               # Main Activity (View)
│   │   └── MainViewModel.kt              # Main ViewModel
│   ├── navgraph/                         # Navigation
│   │   ├── NavGraph.kt                   # Navigation graph setup
│   │   └── Route.kt                      # Navigation routes
│   ├── news_navigator/                   # News Navigation Feature
│   │   ├── components/                   # Navigation components
│   │   │   └── NewsBottomNavigation.kt   # Bottom navigation bar
│   │   └── NewsNavigator.kt              # Navigation container
│   ├── onboarding/                       # Onboarding Feature (MVVM)
│   │   ├── components/                   # Feature-specific components
│   │   │   ├── OnBoardingPage.kt         # Individual onboarding page
│   │   │   └── PagerIndicator.kt         # Page indicator component
│   │   ├── OnBoardingEvent.kt            # User events/actions
│   │   ├── OnBoardingScreen.kt           # VIEW - Compose UI
│   │   ├── OnBoardingViewModel.kt        # VIEWMODEL - Business Logic
│   │   └── Page.kt                       # Page model
│   ├── search/                           # Search Feature (MVVM)
│   │   ├── SearchEvent.kt                # User events/actions
│   │   ├── SearchScreen.kt               # VIEW - Compose UI
│   │   ├── SearchState.kt                # MODEL - UI State
│   │   └── SearchViewModel.kt            # VIEWMODEL - Business Logic
│   └── Dimens.kt                         # UI dimensions constants
├── ui/                                   # UI THEME LAYER
│   └── theme/                            # App theming
│       ├── Color.kt                      # Color definitions
│       ├── Theme.kt                      # Theme configuration
│       └── Type.kt                       # Typography definitions
├── util/                                 # UTILITY LAYER
│   ├── Constants.kt                      # App constants
│   └── DataState.kt                      # Data state classes
└── NewsApplication.kt                    # Application class
```

## MVVM Pattern Implementation

### 1. **Model (State Classes)**
- **Location**: `presentation/*/State.kt` files
- **Purpose**: Represents the UI state and data
- **Examples**: `HomeState.kt`, `SearchState.kt`, `BookmarkState.kt`

### 2. **View (Compose Screens)**
- **Location**: `presentation/*/Screen.kt` files
- **Purpose**: UI layer built with Jetpack Compose
- **Examples**: `HomeScreen.kt`, `SearchScreen.kt`, `BookmarkScreen.kt`

### 3. **ViewModel**
- **Location**: `presentation/*/ViewModel.kt` files
- **Purpose**: Business logic, state management, and use case orchestration
- **Examples**: `HomeViewModel.kt`, `SearchViewModel.kt`, `BookmarkViewModel.kt`

### 4. **Events (User Actions)**
- **Location**: `presentation/*/Event.kt` files
- **Purpose**: Defines user interactions and events
- **Examples**: `DetailsEvent.kt`, `SearchEvent.kt`, `OnBoardingEvent.kt`

## Clean Architecture Layers

### 1. **Data Layer** 📁 `data/`
- **Responsibility**: Data access and external APIs
- **Components**:
  - **Local**: Room database implementation
  - **Remote**: Retrofit API calls and DTOs
  - **Repository**: Data source coordination
  - **Manager**: Data management implementations

### 2. **Domain Layer** 📁 `domain/`
- **Responsibility**: Business logic and rules (framework-independent)
- **Components**:
  - **Models**: Core business entities
  - **Use Cases**: Business operations
  - **Repository Interfaces**: Data access contracts
  - **Manager Interfaces**: Service contracts

### 3. **Presentation Layer** 📁 `presentation/`
- **Responsibility**: UI and user interactions (MVVM implementation)
- **Components**:
  - **Screens**: Jetpack Compose UI
  - **ViewModels**: UI logic and state management
  - **States**: UI state representations
  - **Events**: User action definitions

### 4. **Dependency Injection Layer** 📁 `di/`
- **Responsibility**: Dependency management with Dagger Hilt
- **Components**:
  - **AppModule**: App-level dependencies
  - **RepositoryModule**: Repository bindings
  - **ManagerModule**: Manager implementations

## Key Technologies Used

- **🏗️ Architecture**: MVVM + Clean Architecture
- **🎨 UI Framework**: Jetpack Compose
- **💉 Dependency Injection**: Dagger Hilt
- **🗄️ Local Database**: Room
- **🌐 Networking**: Retrofit + Gson
- **📄 Pagination**: Paging 3
- **🎯 Navigation**: Navigation Compose
- **📊 State Management**: Compose State + ViewModel
- **🖼️ Image Loading**: Coil
- **💾 Preferences**: DataStore

## Benefits of This Architecture

1. **Separation of Concerns**: Each layer has a specific responsibility
2. **Testability**: Easy to unit test business logic
3. **Maintainability**: Changes in one layer don't affect others
4. **Scalability**: Easy to add new features
5. **Reusability**: Domain layer can be reused across platforms
6. **Dependency Rule**: Inner layers don't depend on outer layers
