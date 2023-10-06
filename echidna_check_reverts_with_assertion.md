When You Need to Check if Function Reverts But at the same time the function has arguments,
In that case You can't run it without assertion mode
=

**EDIT: HOLY SHIT HOW DUMB I WAS, SAME CAN BE DONE WITH THIS**
```solidity
 function test_assertion(uint256 amount) public {
        try target.challenge(amount) {
            assert(true);
        } catch {
            assert(false);
        }
    }
```
**hahaha**


```solidity
pragma solidity 0.8.4;

contract vuln {
    function challenge(uint256 amount) public {
        require(amount != 33);
    }
}

contract test {
    vuln target = new vuln();

    function test_assertion(uint256 amount) internal returns (bool) {
        try target.challenge(amount) {
            return true;
        } catch {
            return false;
        }
    }

    function test_big(uint256 amount) public {
        bool catcher = test_assertion(amount);
        assert(catcher == true);
    }
}
```
