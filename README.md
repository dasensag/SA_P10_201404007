# P10 Software Avanzado

Service orchestration with a simple ESB. 

### Usage example video




### Microservices

* **Client:** Sends orders to restaurant, checks order and delivery status.
* **Restaurant:** Recieves orders from client and gives status. Can send orders to deliver.
* **Delivery:** Recieves orders to deliver from restaurant and gives status to client. Can notify when order is delivered.
* **ESB:** Routes requests between the other microservices.

## Requirements

* docker
* docker-compose

# Usage 

First build images with:

`docker-compose build`

Then start containers:

`docker-compose up`

Call the client API exposed on port 3000

`http://localhost:3000`

# Services 

## Client

**POST /order**

Creates a new order

**GET /order/{orderID}**

Checks order status

**GET /delivery/{orderID}**

Checks delivery status

## Restaurant 

**POST /order**

Recieves an order

**GET /order/{orderID}**

Checks order status

**PUT /delivery/{orderID}**

Sends order to delivery

## Delivery

**POST /delivery**

Recieves an order for delivery

**GET /delivery/{orderID}**

Returns delivery status

**PUT /delivery/{orderID}**

Updates delivery status to _delivered_

## ESB

**GET /order/{orderID}**

Recieves request to check order status, routes it to `restaurant` and returns response to `client`

**POST /order**

Recieves a new order from client, sends it to `restaurant` and returns response to `client`

**GET /delivery/{orderID}**

Recieves request to check delivery status, sends it to `deivery` and returns response to `client`

**POST /delivery**

Recieves a new delivery from `restaurant`, sends it to `delivery` and returns response to `restaurant`