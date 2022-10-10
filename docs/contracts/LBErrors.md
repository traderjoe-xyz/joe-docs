---
sidebar_position: 5
sidebar_label: LBErrors
---

## LBRouter__SenderIsNotWAVAX

```solidity
error LBRouter__SenderIsNotWAVAX()
```

LBRouter errors

## LBRouter__PairNotCreated

```solidity
error LBRouter__PairNotCreated(contract IERC20 tokenX, contract IERC20 tokenY, uint256 binStep)
```

## LBRouter__WrongAmounts

```solidity
error LBRouter__WrongAmounts(uint256 amount, uint256 reserve)
```

## LBRouter__SwapOverflows

```solidity
error LBRouter__SwapOverflows(uint256 id)
```

## LBRouter__BrokenSwapSafetyCheck

```solidity
error LBRouter__BrokenSwapSafetyCheck()
```

## LBRouter__NotFactoryOwner

```solidity
error LBRouter__NotFactoryOwner()
```

## LBRouter__TooMuchTokensIn

```solidity
error LBRouter__TooMuchTokensIn(uint256 excess)
```

## LBRouter__BinReserveOverflows

```solidity
error LBRouter__BinReserveOverflows(uint256 id)
```

## LBRouter__IdOverflows

```solidity
error LBRouter__IdOverflows(int256 id)
```

## LBRouter__LengthsMismatch

```solidity
error LBRouter__LengthsMismatch()
```

## LBRouter__WrongTokenOrder

```solidity
error LBRouter__WrongTokenOrder()
```

## LBRouter__IdSlippageCaught

```solidity
error LBRouter__IdSlippageCaught(uint256 activeIdDesired, uint256 idSlippage, uint256 activeId)
```

## LBRouter__AmountSlippageCaught

```solidity
error LBRouter__AmountSlippageCaught(uint256 amountXMin, uint256 amountX, uint256 amountYMin, uint256 amountY)
```

## LBRouter__IdDesiredOverflows

```solidity
error LBRouter__IdDesiredOverflows(uint256 idDesired, uint256 idSlippage)
```

## LBRouter__FailedToSendAVAX

```solidity
error LBRouter__FailedToSendAVAX(address recipient, uint256 amount)
```

## LBRouter__DeadlineExceeded

```solidity
error LBRouter__DeadlineExceeded(uint256 deadline, uint256 currentTimestamp)
```

## LBRouter__AmountSlippageBPTooBig

```solidity
error LBRouter__AmountSlippageBPTooBig(uint256 amountSlippage)
```

## LBRouter__InsufficientAmountOut

```solidity
error LBRouter__InsufficientAmountOut(uint256 amountOutMin, uint256 amountOut)
```

## LBRouter__MaxAmountInExceeded

```solidity
error LBRouter__MaxAmountInExceeded(uint256 amountInMax, uint256 amountIn)
```

## LBRouter__InvalidTokenPath

```solidity
error LBRouter__InvalidTokenPath(contract IERC20 wrongToken)
```

## LBRouter__InvalidVersion

```solidity
error LBRouter__InvalidVersion(uint256 version)
```

## LBRouter__WrongAvaxLiquidityParameters

```solidity
error LBRouter__WrongAvaxLiquidityParameters(contract IERC20 tokenX, contract IERC20 tokenY, uint256 amountX, uint256 amountY, uint256 msgValue)
```

## LBToken__SpenderNotApproved

```solidity
error LBToken__SpenderNotApproved(address owner, address spender)
```

LBToken errors

## LBToken__TransferFromOrToAddress0

```solidity
error LBToken__TransferFromOrToAddress0()
```

## LBToken__MintToAddress0

```solidity
error LBToken__MintToAddress0()
```

## LBToken__BurnFromAddress0

```solidity
error LBToken__BurnFromAddress0()
```

## LBToken__BurnExceedsBalance

```solidity
error LBToken__BurnExceedsBalance(address from, uint256 id, uint256 amount)
```

## LBToken__LengthMismatch

```solidity
error LBToken__LengthMismatch(uint256 accountsLength, uint256 idsLength)
```

## LBToken__SelfApproval

```solidity
error LBToken__SelfApproval(address owner)
```

## LBToken__TransferExceedsBalance

```solidity
error LBToken__TransferExceedsBalance(address from, uint256 id, uint256 amount)
```

## LBFactory__IdenticalAddresses

```solidity
error LBFactory__IdenticalAddresses(contract IERC20 token)
```

LBFactory errors

## LBFactory__QuoteAssetNotWhitelisted

```solidity
error LBFactory__QuoteAssetNotWhitelisted(contract IERC20 quoteAsset)
```

## LBFactory__QuoteAssetAlreadyWhitelisted

```solidity
error LBFactory__QuoteAssetAlreadyWhitelisted(contract IERC20 quoteAsset)
```

## LBFactory__AddressZero

```solidity
error LBFactory__AddressZero()
```

## LBFactory__LBPairAlreadyExists

```solidity
error LBFactory__LBPairAlreadyExists(contract IERC20 tokenX, contract IERC20 tokenY, uint256 _binStep)
```

## LBFactory__LBPairNotCreated

```solidity
error LBFactory__LBPairNotCreated(contract IERC20 tokenX, contract IERC20 tokenY, uint256 binStep)
```

## LBFactory__DecreasingPeriods

```solidity
error LBFactory__DecreasingPeriods(uint16 filterPeriod, uint16 decayPeriod)
```

## LBFactory__BaseFactorOverflows

```solidity
error LBFactory__BaseFactorOverflows(uint16 baseFactor, uint256 max)
```

## LBFactory__ReductionFactorOverflows

```solidity
error LBFactory__ReductionFactorOverflows(uint16 reductionFactor, uint256 max)
```

## LBFactory__VariableFeeControlOverflows

```solidity
error LBFactory__VariableFeeControlOverflows(uint16 variableFeeControl, uint256 max)
```

## LBFactory__BaseFeesBelowMin

```solidity
error LBFactory__BaseFeesBelowMin(uint256 baseFees, uint256 minBaseFees)
```

## LBFactory__FeesAboveMax

```solidity
error LBFactory__FeesAboveMax(uint256 fees, uint256 maxFees)
```

## LBFactory__BinStepRequirementsBreached

```solidity
error LBFactory__BinStepRequirementsBreached(uint256 lowerBound, uint16 binStep, uint256 higherBound)
```

## LBFactory__ProtocolShareOverflows

```solidity
error LBFactory__ProtocolShareOverflows(uint16 protocolShare, uint256 max)
```

## LBFactory__FunctionIsLockedForUsers

```solidity
error LBFactory__FunctionIsLockedForUsers(address user)
```

## LBFactory__FactoryLockIsAlreadyInTheSameState

```solidity
error LBFactory__FactoryLockIsAlreadyInTheSameState()
```

## LBFactory__LBPairIgnoredIsAlreadyInTheSameState

```solidity
error LBFactory__LBPairIgnoredIsAlreadyInTheSameState()
```

## LBFactory__BinStepHasNoPreset

```solidity
error LBFactory__BinStepHasNoPreset(uint256 binStep)
```

## LBFactory__SameFeeRecipient

```solidity
error LBFactory__SameFeeRecipient(address feeRecipient)
```

## LBFactory__SameFlashLoanFee

```solidity
error LBFactory__SameFlashLoanFee(uint256 flashLoanFee)
```

## LBFactory__LBPairSafetyCheckFailed

```solidity
error LBFactory__LBPairSafetyCheckFailed(address LBPairImplementation)
```

## LBFactory__SameImplementation

```solidity
error LBFactory__SameImplementation(address LBPairImplementation)
```

## LBFactory__ImplementationNotSet

```solidity
error LBFactory__ImplementationNotSet()
```

## LBPair__InsufficientAmounts

```solidity
error LBPair__InsufficientAmounts()
```

LBPair errors

## LBPair__AddressZero

```solidity
error LBPair__AddressZero()
```

## LBPair__BrokenSwapSafetyCheck

```solidity
error LBPair__BrokenSwapSafetyCheck()
```

## LBPair__CompositionFactorFlawed

```solidity
error LBPair__CompositionFactorFlawed(uint256 id)
```

## LBPair__InsufficientLiquidityMinted

```solidity
error LBPair__InsufficientLiquidityMinted(uint256 id)
```

## LBPair__InsufficientLiquidityBurned

```solidity
error LBPair__InsufficientLiquidityBurned(uint256 id)
```

## LBPair__WrongLengths

```solidity
error LBPair__WrongLengths()
```

## LBPair__OnlyStrictlyIncreasingId

```solidity
error LBPair__OnlyStrictlyIncreasingId()
```

## LBPair__OnlyFactory

```solidity
error LBPair__OnlyFactory()
```

## LBPair__DistributionsOverflow

```solidity
error LBPair__DistributionsOverflow()
```

## LBPair__OnlyFeeRecipient

```solidity
error LBPair__OnlyFeeRecipient(address feeRecipient, address sender)
```

## LBPair__OracleNotEnoughSample

```solidity
error LBPair__OracleNotEnoughSample()
```

## LBPair__FlashLoanCallbackFailed

```solidity
error LBPair__FlashLoanCallbackFailed()
```

## LBPair__AlreadyInitialized

```solidity
error LBPair__AlreadyInitialized()
```

## LBPair__NewSizeTooSmall

```solidity
error LBPair__NewSizeTooSmall(uint256 newSize, uint256 oracleSize)
```

## BinHelper__BinStepOverflows

```solidity
error BinHelper__BinStepOverflows(uint256 bp)
```

BinHelper errors

## BinHelper__IdOverflows

```solidity
error BinHelper__IdOverflows(int256 id)
```

## BinHelper__IntOverflows

```solidity
error BinHelper__IntOverflows(uint256 id)
```

## FeeDistributionHelper__FlashLoanUnderflow

```solidity
error FeeDistributionHelper__FlashLoanUnderflow(uint256 expectedBalance, uint256 balance)
```

FeeDistributionHelper errors

## Math128x128__PowerUnderflow

```solidity
error Math128x128__PowerUnderflow(uint256 x, int256 y)
```

Math128x128 errors

## Math128x128__LogUnderflow

```solidity
error Math128x128__LogUnderflow()
```

## Math512Bits__MulDivOverflow

```solidity
error Math512Bits__MulDivOverflow(uint256 prod1, uint256 denominator)
```

Math512Bits errors

## Math512Bits__ShiftDivOverflow

```solidity
error Math512Bits__ShiftDivOverflow(uint256 prod1, uint256 denominator)
```

## Math512Bits__MulShiftOverflow

```solidity
error Math512Bits__MulShiftOverflow(uint256 prod1, uint256 offset)
```

## Math512Bits__OffsetOverflows

```solidity
error Math512Bits__OffsetOverflows(uint256 offset)
```

## Oracle__AlreadyInitialized

```solidity
error Oracle__AlreadyInitialized(uint256 _index)
```

Oracle errors

## Oracle__LookUpTimestampTooOld

```solidity
error Oracle__LookUpTimestampTooOld(uint256 _minTimestamp, uint256 _lookUpTimestamp)
```

## Oracle__NotInitialized

```solidity
error Oracle__NotInitialized()
```

## PendingOwnable__NotOwner

```solidity
error PendingOwnable__NotOwner()
```

PendingOwnable errors

## PendingOwnable__NotPendingOwner

```solidity
error PendingOwnable__NotPendingOwner()
```

## PendingOwnable__PendingOwnerAlreadySet

```solidity
error PendingOwnable__PendingOwnerAlreadySet()
```

## PendingOwnable__NoPendingOwner

```solidity
error PendingOwnable__NoPendingOwner()
```

## PendingOwnable__AddressZero

```solidity
error PendingOwnable__AddressZero()
```

## ReentrancyGuardUpgradeable__ReentrantCall

```solidity
error ReentrancyGuardUpgradeable__ReentrantCall()
```

ReentrancyGuardUpgradeable errors

## ReentrancyGuardUpgradeable__AlreadyInitialized

```solidity
error ReentrancyGuardUpgradeable__AlreadyInitialized()
```

## SafeCast__Exceeds256Bits

```solidity
error SafeCast__Exceeds256Bits(uint256 x)
```

SafeCast errors

## SafeCast__Exceeds248Bits

```solidity
error SafeCast__Exceeds248Bits(uint256 x)
```

## SafeCast__Exceeds240Bits

```solidity
error SafeCast__Exceeds240Bits(uint256 x)
```

## SafeCast__Exceeds232Bits

```solidity
error SafeCast__Exceeds232Bits(uint256 x)
```

## SafeCast__Exceeds224Bits

```solidity
error SafeCast__Exceeds224Bits(uint256 x)
```

## SafeCast__Exceeds216Bits

```solidity
error SafeCast__Exceeds216Bits(uint256 x)
```

## SafeCast__Exceeds208Bits

```solidity
error SafeCast__Exceeds208Bits(uint256 x)
```

## SafeCast__Exceeds200Bits

```solidity
error SafeCast__Exceeds200Bits(uint256 x)
```

## SafeCast__Exceeds192Bits

```solidity
error SafeCast__Exceeds192Bits(uint256 x)
```

## SafeCast__Exceeds184Bits

```solidity
error SafeCast__Exceeds184Bits(uint256 x)
```

## SafeCast__Exceeds176Bits

```solidity
error SafeCast__Exceeds176Bits(uint256 x)
```

## SafeCast__Exceeds168Bits

```solidity
error SafeCast__Exceeds168Bits(uint256 x)
```

## SafeCast__Exceeds160Bits

```solidity
error SafeCast__Exceeds160Bits(uint256 x)
```

## SafeCast__Exceeds152Bits

```solidity
error SafeCast__Exceeds152Bits(uint256 x)
```

## SafeCast__Exceeds144Bits

```solidity
error SafeCast__Exceeds144Bits(uint256 x)
```

## SafeCast__Exceeds136Bits

```solidity
error SafeCast__Exceeds136Bits(uint256 x)
```

## SafeCast__Exceeds128Bits

```solidity
error SafeCast__Exceeds128Bits(uint256 x)
```

## SafeCast__Exceeds120Bits

```solidity
error SafeCast__Exceeds120Bits(uint256 x)
```

## SafeCast__Exceeds112Bits

```solidity
error SafeCast__Exceeds112Bits(uint256 x)
```

## SafeCast__Exceeds104Bits

```solidity
error SafeCast__Exceeds104Bits(uint256 x)
```

## SafeCast__Exceeds96Bits

```solidity
error SafeCast__Exceeds96Bits(uint256 x)
```

## SafeCast__Exceeds88Bits

```solidity
error SafeCast__Exceeds88Bits(uint256 x)
```

## SafeCast__Exceeds80Bits

```solidity
error SafeCast__Exceeds80Bits(uint256 x)
```

## SafeCast__Exceeds72Bits

```solidity
error SafeCast__Exceeds72Bits(uint256 x)
```

## SafeCast__Exceeds64Bits

```solidity
error SafeCast__Exceeds64Bits(uint256 x)
```

## SafeCast__Exceeds56Bits

```solidity
error SafeCast__Exceeds56Bits(uint256 x)
```

## SafeCast__Exceeds48Bits

```solidity
error SafeCast__Exceeds48Bits(uint256 x)
```

## SafeCast__Exceeds40Bits

```solidity
error SafeCast__Exceeds40Bits(uint256 x)
```

## SafeCast__Exceeds32Bits

```solidity
error SafeCast__Exceeds32Bits(uint256 x)
```

## SafeCast__Exceeds24Bits

```solidity
error SafeCast__Exceeds24Bits(uint256 x)
```

## SafeCast__Exceeds16Bits

```solidity
error SafeCast__Exceeds16Bits(uint256 x)
```

## SafeCast__Exceeds8Bits

```solidity
error SafeCast__Exceeds8Bits(uint256 x)
```

## TreeMath__ErrorDepthSearch

```solidity
error TreeMath__ErrorDepthSearch()
```

TreeMath errors

## JoeLibrary__IdenticalAddresses

```solidity
error JoeLibrary__IdenticalAddresses()
```

JoeLibrary errors

## JoeLibrary__AddressZero

```solidity
error JoeLibrary__AddressZero()
```

## JoeLibrary__InsufficientAmount

```solidity
error JoeLibrary__InsufficientAmount()
```

## JoeLibrary__InsufficientLiquidity

```solidity
error JoeLibrary__InsufficientLiquidity()
```

## TokenHelper__TransferFailed

```solidity
error TokenHelper__TransferFailed(contract IERC20 token, address recipient, uint256 amount)
```

TokenHelper errors

## LBQuoter_InvalidLength

```solidity
error LBQuoter_InvalidLength()
```

LBQuoter errors

