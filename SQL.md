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
