# Test File Format for Orderbook Test Suite

This README provides an overview of the structure and components of the `.txt` files used for testing the Orderbook system. Each file represents a specific test scenario and is designed to validate different aspects of order management, such as adding, modifying, canceling, and matching orders.

## File Structure

Each `.txt` test file consists of a series of lines, where each line describes either an action to be performed on the orderbook or the expected result after all actions have been executed. The file is processed line by line in the order provided.

### Action Lines

An action line specifies an operation to be performed on the orderbook. There are three types of actions:

1. **Add Order**
2. **Modify Order**
3. **Cancel Order**

#### 1. Add Order

An "Add" action adds a new order to the orderbook. The format is as follows:

`A <Side> <OrderType> <Price> <Quantity> <OrderId>`

- `A`: Indicates an "Add" action.
- `<Side>`: The side of the order, either `B` for Buy or `S` for Sell.
- `<OrderType>`: The type of order, which can be one of the following:
  - `FillAndKill`
  - `GoodTillCancel`
  - `GoodForDay`
  - `FillOrKill`
  - `Market`
- `<Price>`: The price of the order.
- `<Quantity>`: The quantity of the order.
- `<OrderId>`: A unique identifier for the order.

**Example:**
`A B GoodTillCancel 100 10 1`

This line adds a Buy order of type `GoodTillCancel` with a price of 100, quantity of 10, and an order ID of 1.

#### 2. Modify Order

A "Modify" action modifies an existing order in the orderbook. The format is as follows:
`M <OrderId> <Side> <Price> <Quantity>`

- `M`: Indicates a "Modify" action.
- `<OrderId>`: The unique identifier of the order to be modified.
- `<Side>`: The side of the order (`B` for Buy, `S` for Sell).
- `<Price>`: The new price of the order.
- `<Quantity>`: The new quantity of the order.

**Example:**
`M 1 B 105 15`

This line modifies the order with ID 1 to have a new price of 105 and a new quantity of 15.

#### 3. Cancel Order

A "Cancel" action cancels an existing order in the orderbook. The format is as follows:

`C <OrderId>`

- `C`: Indicates a "Cancel" action.
- `<OrderId>`: The unique identifier of the order to be canceled.

**Example:**
`C 1`

This line cancels the order with ID 1.

### Result Line

The result line specifies the expected state of the orderbook after all actions have been performed. There should be exactly one result line in each test file, and it must be the last line of the file.
`R <AllCount> <BidCount> <AskCount>`

- `R`: Indicates a result line.
- `<AllCount>`: The total number of orders expected in the orderbook.
- `<BidCount>`: The total number of Buy (Bid) orders expected in the orderbook.
- `<AskCount>`: The total number of Sell (Ask) orders expected in the orderbook.

**Example:**
`R 2 1 1`

This line indicates that after all actions, the orderbook should contain 2 orders in total, with 1 Buy order and 1 Sell order.

## Example Test File

Below is an example of a complete test file:

```
A B GoodTillCancel 100 10 1
A S Market 101 5 2
M 1 B 105 15
C 2
R 1 1 0
```

- **Line 1**: Adds a Buy order with ID 1.
- **Line 2**: Adds a Sell order with ID 2.
- **Line 3**: Modifies the Buy order with ID 1.
- **Line 4**: Cancels the Sell order with ID 2.
- **Line 5**: The result line, indicating that 1 Buy order remains in the orderbook, and there are no Sell orders.

## Notes

- Each test file must end with a result line.
- The order of actions matters and will affect the final state of the orderbook.
- If an order ID does not exist for a Modify or Cancel action, the behavior depends on the implementation of the Orderbook system (which may throw an error or handle it gracefully).

By following this format, you can create comprehensive test cases that cover a wide range of scenarios to validate the functionality of your Orderbook system.
