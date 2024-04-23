# sql

CREATE TABLE `account` (

  `user_id` varchar(8) COLLATE utf8mb3_unicode_ci NOT NULL,

  `user_pwd` varchar(15) COLLATE utf8mb3_unicode_ci NOT NULL,

  `user_role` tinyint DEFAULT NULL,

  PRIMARY KEY (`user_id`)

) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3 COLLATE=utf8mb3_unicode_ci;



CREATE TABLE `all_tables` (

  `table_id` tinyint NOT NULL AUTO_INCREMENT,

  `table_status` tinyint DEFAULT '0',

  `table_capacity` tinyint DEFAULT NULL,

  PRIMARY KEY (`table_id`)

) ENGINE=InnoDB AUTO_INCREMENT=13 DEFAULT CHARSET=utf8mb3 COLLATE=utf8mb3_unicode_ci;



CREATE TABLE `all_menus` (

  `menu_id` int NOT NULL AUTO_INCREMENT,

  `menu_photo` mediumblob,

  `menu_name` varchar(255) COLLATE utf8mb3_unicode_ci DEFAULT NULL,

  `menu_price` varchar(10) COLLATE utf8mb3_unicode_ci DEFAULT NULL,

  `menu_category` tinyint DEFAULT NULL,

  `menu_detail` varchar(255) COLLATE utf8mb3_unicode_ci DEFAULT NULL,

  `status_of_stock` tinyint DEFAULT NULL,

  PRIMARY KEY (`menu_id`)

) ENGINE=InnoDB AUTO_INCREMENT=22 DEFAULT CHARSET=utf8mb3 COLLATE=utf8mb3_unicode_ci;



CREATE TABLE `customer_info` (

  `customer_id` int NOT NULL AUTO_INCREMENT,

  `customer_name` varchar(255) COLLATE utf8mb3_unicode_ci DEFAULT NULL,

  `total_people` tinyint DEFAULT NULL,

  `check_status` tinyint DEFAULT '0',

  `checkin_time` timestamp NULL DEFAULT NULL,

  `checkout_time` timestamp NULL DEFAULT NULL,

  `table_id` tinyint DEFAULT NULL,

  PRIMARY KEY (`customer_id`),

  UNIQUE KEY `customer_id` (`customer_id`),

  KEY `table_id` (`table_id`),

  CONSTRAINT `customer_info_ibfk_1` FOREIGN KEY (`table_id`) REFERENCES `all_tables` (`table_id`)

) ENGINE=InnoDB AUTO_INCREMENT=14 DEFAULT CHARSET=utf8mb3 COLLATE=utf8mb3_unicode_ci;



CREATE TABLE `orders` (

  `order_id` int NOT NULL AUTO_INCREMENT,

  `order_quantity` tinyint NOT NULL,

  `order_status` tinyint NOT NULL DEFAULT '0',

  `order_item_name` varchar(255) COLLATE utf8mb3_unicode_ci DEFAULT NULL,

  `table_id` tinyint DEFAULT NULL,

  `customer_id` int DEFAULT NULL,

  `order_item_price` int DEFAULT NULL,

  PRIMARY KEY (`order_id`),

  KEY `table_id` (`table_id`),

  KEY `customer_id` (`customer_id`),

  CONSTRAINT `orders_ibfk_1` FOREIGN KEY (`table_id`) REFERENCES `all_tables` (`table_id`),

  CONSTRAINT `orders_ibfk_2` FOREIGN KEY (`customer_id`) REFERENCES `customer_info` (`customer_id`)

) ENGINE=InnoDB AUTO_INCREMENT=27 DEFAULT CHARSET=utf8mb3 COLLATE=utf8mb3_unicode_ci;
