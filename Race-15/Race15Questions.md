[Q1] What is/are the correct implementation(s) of the nonReentrant() modifier?  
(A): 
require (reentrancy_lock == 1); 
       reentrancy_lock = 0;
        _;
       reentrancy_lock = 1;
Correct
(B): 
require (reentrancy_lock == 0); 
       reentrancy_lock = 1;
        _;
       reentrancy_lock = 0;
Correct
(C): 
require (reentrancy_lock == 1); 
       reentrancy_lock = 1;
        _;
       reentrancy_lock = 0;

(D): 
require (reentrancy_lock == 0); 
       reentrancy_lock = 2;
       _;
       reentrancy_lock = 0;

[Q2] Who can claim fees using claimFees()?
(A): Only the owner, due to onlyOwner modifier
(B): The owner 
(C): Anyone who can trick owner into signing an arbitrary transaction
(D): No one 
     
[Q3] In buyEth(), we put an unchecked block on “current_eth -= amount”:
(A): Because current_eth is uint
(B): Because the compiler is protecting us from overflows
(C): Only if we add a prior check:
    require(current_eth > amount);
(D): Only if we add a prior check:
    require(current_eth >= amount);

[Q4] In buyEth(), are there any reentrancy concerns assuming the nonReentrant modifier is implemented correctly? 
(A): No, because it has the nonReentrant modifier
(B): No, and even without the modifier you can't exploit any issue 
(C): Yes, there is a cross-contract reentrancy concern via Seller 
(D): None of the above

[Q5] What will happen when calling buyEth() via SimpleDexProxy?
(A): buyEth() will be called and successfully executed 
(B): You can’t call a function that way; it must be called directly
(C): buyEth() will be called but ETH won't be transferred
(D): Transaction will be reverted

[Q6] In buyEth():
(A): If amount is less than 100, it will lead to an incorrect calculation of fee
(B): If token_balance is already at its MAX_UINT256, it will result in overflow and won't revert
(C): If token_amount is > MAX_UINT64, it will result in a casting issue
(D): None of the above

[Q7] Can getEthPrice() return zero?
(A): Yes, if the owner initializes the contract with more ETH than token_balance
(B)  Yes, a carefully crafted buyEth() transaction can result in getEthPrice() returning zero
(C): Yes, once all the ETH are sold
(D): No, there is no issue

[Q8] Which of the following invariants (written in propositional logic) hold on a correct implementation of the code?
(A): this.balance == current_eth <=> token.balanceOf(this) == token_balance
(B): this.balance >= current_eth && token.balanceOf(this) >= token_balance
(C): this.balance <= token.balanceOf(this) &&  token.balanceOf(this) <= token_balance
(D): this.balance >= current_eth || token.balanceOf(this)  >= token_balance