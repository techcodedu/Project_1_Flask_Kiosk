```
CREATE TABLE `product` (
  `ProductID` int(11) NOT NULL,
  `ProductName` varchar(255) DEFAULT NULL,
  `Price` decimal(10,2) DEFAULT NULL,
  `Unit` varchar(50) DEFAULT NULL,
  `PhotoURL` varchar(255) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

INSERT INTO `product` (`ProductID`, `ProductName`, `Price`, `Unit`, `PhotoURL`) VALUES
(1, 'Fresh Apples', 2.50, 'kg', 'images/apple.jpg'),
(2, 'Organic Tomatoes', 3.00, 'kg', 'images/orange.jpg'),
(3, 'Green Lettuce', 1.20, 'piece', '../assets/images/noche.jpg'),
(4, 'Whole Wheat Bread', 2.00, 'pack', '../assets/images/buffalo.jpg'),
(5, 'Free Range Eggs', 3.50, 'dozen', 'images/eggs.jpg');

ALTER TABLE `product`
ADD PRIMARY KEY (`ProductID`);

ALTER TABLE `product`
  MODIFY `ProductID` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=6;
```
```
CREATE TABLE `order` (
  `OrderID` int(11) NOT NULL,
  `CustomerMobileNumber` varchar(15) DEFAULT NULL,
  `TotalCost` decimal(10,2) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

ALTER TABLE `order`
  ADD PRIMARY KEY (`OrderID`);
```
```
CREATE TABLE `orderdetails` (
  `OrderDetailsID` int(11) NOT NULL,
  `OrderID` int(11) NOT NULL,
  `ProductID` int(11) NOT NULL,
  `Quantity` decimal(10,2) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

ALTER TABLE `orderdetails`
  ADD PRIMARY KEY (`OrderDetailsID`),
  ADD KEY `OrderID` (`OrderID`),
  ADD KEY `ProductID` (`ProductID`);
```
