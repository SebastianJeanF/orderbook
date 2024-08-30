# Orderbook and Matching Engine

## Project Overview

This project implements an efficient orderbook and matching engine in C++. It's designed to scalably handle order placement, cancellation, and modification in a financial trading environment.

## Key Features

- Support for multiple order types (GoodTillCancel, FillAndKill, FillOrKill, GoodForDay, Market)
- Efficient matching algorithm for order execution
- Thread-safe operations with mutex locks
- Automatic pruning of expired GoodForDay orders
- Comprehensive order and trade information tracking

## Project Structure

The project consists of several key components:

- `Orderbook`: The main class handling order management and matching
- `Order`: Represents individual orders with their properties and states
- `OrderModify`: Handles order modification requests
- `Trade`: Represents executed trades
- `Constants`: Defines global constants used in the project
- `LevelInfo` and `OrderbookLevelInfos`: Provide information about order book levels


## Performance Considerations

- The project leverages efficient data structures for optimal performance:
  - `std::unordered_map` for quick access to level data and order entries by price and OrderId respectively (O(1) average case lookup).
  - `std::map` for maintaining sorted bid and ask orders, allowing for efficient order matching and best price determination (O(log n) for insertion, deletion, and finding the best price, with n being the number of unique price levels in the book).
  - `std::list` for storing orders at each price level, enabling fast insertion and deletion of orders (O(1) when the position is known).

- Modern C++ features are utilized throughout the project:
  - Smart pointers (`std::shared_ptr`) for automatic memory management of orders.
  - Scoped locks (`std::mutex` and `std::lock_guard`) for thread-safe operations.
  - Move semantics and perfect forwarding to minimize unnecessary copying.

- The order book structure is designed for fast lookups and updates:
  - Separate collections for bids and asks allow for quick access to the best prices.
  - Price levels are indexed for rapid order placement and cancellation.

- Efficient matching algorithm:
  - Orders are stored in price-time priority, allowing for fair and quick matching.
  - Partial fills are supported without sacrificing performance.

- Automatic pruning of expired orders:
  - A separate thread handles the removal of GoodForDay orders, preventing the order book from accumulating stale orders without impacting the main execution path.

- Use of `std::atomic` for thread-safe shutdown flag checking.

These design choices result in a performant orderbook and matching engine capable of handling a large volume of orders and trades without excessive latency.


