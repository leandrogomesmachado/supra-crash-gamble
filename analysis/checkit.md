### Question 01
Why over the line 300 has hardcoded address?

### My thought
People will want to check the public address of the owner for transparency. 
The contract is broken if implemented at another address.
**Exploit**:  VRF oracle will be unable to call `fulfill_randomness`
**Solution**: Use parameter or store dynamically

Possible fix:

```move
// VULNERABLE (Line 300)
let admin_addr = @moon_dog;

// FIX
let admin_addr = game.admin; // use dynamic address
```

### Question 02
Possible Race Condition between lines 296 to 325?

### My thought
The `fulfill_randomness` function does not verify the caller's signature.
**Impact:** **CRITICAL** - Anyone can call and manipulate the outcome.
**Exploit:** Attacker can call with random values ​​to control crash point.
**Solution:** Implement VRF source verification.

## Another questions
User can reentry in cash out because have external calls without reentrancy protection.

Need some small changes (but need to check backend and frontend).