```solidity
pragma solidity 0.8.4;

contract vuln {
    function challenge(uint256 amount) public {
        require(amount != 33);
    }
}

contract test {
    vuln target = new vuln();

    // function echidna_functionIsCallable(uint256 amount) public returns (bool) {
    //     try target.challenge(amount) {
    //         return true;
    //     } catch {
    //         return false;
    //     }
    // }
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
