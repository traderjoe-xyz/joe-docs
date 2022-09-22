---
id: Bin pricing
---


### Getting price from bin ID


Use function in `LBRouter.sol`:

`function getPriceFromId(ILBPair LBPair, uint24 id) external view returns (uint256);`

IDs that can be passed are in range defined by whitepaper and are dependent on bin step of given pair.

Price returned by `getPriceFromId` function is a 128.128-binary fixed-point number

Both `priceScaled >> bitShift` and `priceScaled / 2 ** 128` are correct, but shifting is preferred. 

```js
uint24 _id = 2**23; // Parity ID, where priceX = priceY
uint256 bitShift = 128; 
uint256 _precision = 10e18; // Just an example
uint256 priceScaled;
uint256 price;

// Values will be different for other bin steps. Results below for pair's bin step = 25
priceScaled = router.getPriceFromId(pair, _id); // 340282366920938463463374607431768211456
price = (priceScaled * _precision) >> bitShift; // 10000000000000000000 ~= 1

priceScaled = router.getPriceFromId(pair, _id + 10); // 348885771338866814338043261489323424587
price = (priceScaled * _precision) >> bitShift; // 10252831332277857178 ~= 1.0253

priceScaled = router.getPriceFromId(pair, _id - 10); // 331891119528773528117799799015077021578
price = (priceScaled * _precision) >> bitShift; // 9753403402353946658 ~= 0.9753
```



### Getting bin ID from price

Use function in `LBRouter.sol`:

`function getIdFromPrice(ILBPair LBPair, uint256 price) external view returns (uint24);`

The id may be inaccurate due to rounding issues, always trust getPriceFromId rather than getIdFromPrice

Price passed to  by `getIdFromPrice` function should be a 128.128-binary fixed-point number for maximum precision

Both `priceWanted << bitShift` and `priceWanted * 2 ** 128` are correct, but shifting is preferred. 

```js
uint24 _id = 2**23; // Parity ID, where priceX = priceY
uint256 _precision = 10e18; // Just an example
uint24 id;
uint256 price;
uint256 priceWanted;

// Values will be different for other bin steps. Results for pair bin step = 25
priceWanted = 1 << bitShift;
id = router.getIdFromPrice(pair, priceWanted); // 8388608 = _id

price = 10252831332277857178; // Result from previous point
priceWanted = (price << bitShift) / _precision; 
id = router.getIdFromPrice(pair, priceWanted); // 8388617 = _id + 9
/*
note, that this is not the same result that would be expected based on getPriceFromId function. 
getIdFromPrice falls into rounding issues; always rely on getPriceFromId for precise measure
*/
price = 9753403402353946658; // Result from previous point
priceWanted = (price << bitShift) / _precision; 
id = router.getIdFromPrice(pair, priceWanted); // 8388598 = _id - 10
```