---
id: Bin pricing
---


### Getting price from bin ID


Use function in `LBRouter.sol`:

`function getPriceFromId(ILBPair LBPair, uint24 id) external view returns (uint256);`

IDs that can be passed are in range defined by whitepaper and are dependent on bin step of given pair.

Price returned by `getPriceFromId` function is a 128.128-binary fixed-point number

```js
uint24 _id = 2**23; //parity ID, where priceX = priceY
uint256 denominator = 2**128 - 1; //due to price being 128.128-binary fixed-point number
uint256 _precision = 10e18; //just an example
uint256 priceScaled;
uint256 price;

//Values will be different for other bin steps. Results below for pair's bin step = 25
priceScaled = router.getPriceFromId(pair, _id); //340282366920938463463374607431768211455
price = (priceScaled * _precision) / denominator; //10000000000000000000 = 1

priceScaled = router.getPriceFromId(pair, _id + 10); //348885771338866814338043261489323424587
price = (priceScaled * _precision) / denominator; //10252831332277857178 ~= 1.0252

priceScaled = router.getPriceFromId(pair, _id - 10); //331891119528773528117799799015077021578
price = (priceScaled * _precision) / denominator; //9753403402353946658 ~= 0.9753
```



### Getting bin ID from price

Use function in `LBRouter.sol`:

`function getIdFromPrice(ILBPair LBPair, uint256 price) external view returns (uint24);`

The id may be inaccurate due to rounding issues, always trust getPriceFromId rather than getIdFromPrice

```js
uint24 _id = 2**23; //parity ID, where priceX = priceY
uint256 numerator = 2**128 - 1; //due to price being 128.128-binary fixed-point number
uint256 _precision = 10e18; //just an example
uint24 id;
uint256 priceWanted;
//Values will be different for other bin steps. Results for pair bin step = 25
priceWanted = 1 * numerator;
id = router.getIdFromPrice(pair, priceWanted); //8388608 = _id


priceWanted = (10252831332277857178 * numerator) / _precision; //result from previous point
id = router.getIdFromPrice(pair, priceWanted); //8388617 = _id + 9
/*
note, that this is not the same result that would be expected based on getPriceFromId function. 
getIdFromPrice falls into rounding issues; always rely on getPriceFromId for precise measure
*/

priceWanted = (9753403402353946658 * numerator) / _precision; //result from previous point
id = router.getIdFromPrice(pair, priceWanted); //8388598 = _id - 10
```