# MovieDB With Programmatic UI
A modern iOS application that allows users to browse popular movies, search for specific titles, and view detailed information including cast members. Built with Swift using the MVVM architecture pattern and programmatic UI.

## Features

- **Browse Popular Movies**: Discover trending and popular movies from The Movie Database (TMDB)
- **Search Functionality**: Real-time search to find movies by title
- **Detailed Movie Information**: View comprehensive details including:
  - Movie poster and title
  - Rating and vote count
  - Release date
  - Genres
  - Overview/synopsis
  - Runtime
  - Original language
- **Cast Information**: Browse cast members with profile images in a horizontal scrollable view
- **Clean UI**: Programmatically built interface with custom cells and smooth navigation

## Architecture

This project implements the **MVVM (Model-View-ViewModel)** architecture pattern with protocol-oriented design:

- **Model**: Data structures for movies, details, and credits (`MovieModel`, `MovieDetailModel`, `MovieCreditsModel`)
- **View**: ViewControllers and custom cells built programmatically without storyboards
- **ViewModel**: Business logic and data transformation (`MovieViewModel`, `MovieDetailViewModel`)
- **Service**: Network layer with generic API client using URLSession

### Key Design Patterns

- **Protocol-Oriented Programming**: Protocols for ViewModels, API clients, and endpoints
- **Closure-Based Binding**: ViewModels communicate with Views through closures instead of delegates
- **Dependency Injection**: ViewModels injected into ViewControllers
- **Singleton Pattern**: UI utilities for loading indicators and alerts

## Project Structure

```
YemeksepetiMovieDB/
├── Resources/          # App delegates and configuration
├── Model/              # Data models (Codable structs)
├── View/               # ViewControllers and custom cells
├── ViewModel/          # Business logic and data transformation
├── Service/            # API client and endpoint definitions
└── Common/             # Utility classes and helpers
```

## Requirements

- iOS 10.0+
- Xcode 12.0+
- Swift 5.0+
- CocoaPods

## Dependencies

- **Kingfisher** (4.10.1): Efficient image downloading and caching library
 
### Endpoints Used

- `GET /3/movie/popular` - Fetch popular movies
- `GET /3/movie/{id}` - Fetch movie details
- `GET /3/movie/{id}/credits` - Fetch cast and crew information
- `GET /3/search/movie` - Search movies by query

## Code Highlights

### Generic API Client

```swift
protocol ApiClient {
    func fetch<T: Decodable>(with request: URLRequest,
                            decode: @escaping (Decodable) -> T?,
                            completion: @escaping (Result<T, APIError>) -> Void)
}
```

### Closure-Based Binding

```swift
viewModel.updateUIHandler = { [weak self] in
    DispatchQueue.main.async {
        self?.tableView.reloadData()
    }
}
```

### Programmatic UI

All UI components are created programmatically with Auto Layout:

```swift
view.addSubview(tableView)
tableView.translatesAutoresizingMaskIntoConstraints = false
NSLayoutConstraint.activate([
    tableView.topAnchor.constraint(equalTo: view.topAnchor),
    tableView.leadingAnchor.constraint(equalTo: view.leadingAnchor),
    tableView.trailingAnchor.constraint(equalTo: view.trailingAnchor),
    tableView.bottomAnchor.constraint(equalTo: view.bottomAnchor)
])
```

## Testing

The project includes template files for:
- Unit Tests (`YemeksepetiMovieDBTests`)
- UI Tests (`YemeksepetiMovieDBUITests`)

To run tests: `⌘+U` in Xcode

## Acknowledgments

- Movie data provided by [The Movie Database (TMDB)](https://www.themoviedb.org/)
- Image loading powered by [Kingfisher](https://github.com/onevcat/Kingfisher)
