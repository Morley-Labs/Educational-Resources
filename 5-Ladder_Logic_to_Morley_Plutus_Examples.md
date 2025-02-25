
## 10 Unique Ladder Logic Programs with Structured Text, IR, and Morley Plutus Scripts

---

## Example 1: Start-Stop Circuit (Basic Latching Logic)  

### Ladder Logic  
```
     I1  --| |------( Q1 )   // Start Button (Normally Open Contact)
     I2  --|/|------( Q1 )   // Stop Button (Normally Closed Contact)
     Q1  --| |------( Q1 )   // Latching to keep Motor ON
```

### Structured Text (ST)
```pascal
IF I1 THEN
    Q1 := TRUE;
END_IF;

IF I2 THEN
    Q1 := FALSE;
END_IF;
```

### Intermediate Representation (IR)  
```json
{
  "logic": [
    { "type": "IR_XIC", "input": "I1", "output": "Q1" },
    { "type": "IR_XIO", "input": "I2", "output": "Q1" },
    { "type": "IR_XIC", "input": "Q1", "output": "Q1" }
  ]
}
```

### Morley Plutus Script  
```haskell
{-# INLINABLE startStop #-}
startStop :: BuiltinData -> BuiltinData -> ScriptContext -> Bool
startStop datum redeemer ctx = traceIfFalse "Start-Stop Condition Failed" $
  (inputI1 && not inputI2) || (prevStateQ1 && not inputI2)
  where
    inputI1 = checkInput "I1" ctx
    inputI2 = checkInput "I2" ctx
    prevStateQ1 = checkState "Q1" ctx
```

---

## Example 2: Toggle Output (TOG)  

### Ladder Logic  
```
     I1  --| |------[ TOG Q1 ]
```

### Structured Text (ST)
```pascal
IF I1 THEN
    Q1 := NOT Q1;
END_IF;
```

### Intermediate Representation (IR)  
```json
{
  "logic": [
    { "type": "IR_XIC", "input": "I1", "output": "Q1" },
    { "type": "IR_TOG", "output": "Q1" }
  ]
}
```

### Morley Plutus Script  
```haskell
{-# INLINABLE toggleOutput #-}
toggleOutput :: BuiltinData -> BuiltinData -> ScriptContext -> Bool
toggleOutput datum redeemer ctx = 
  inputI1 && toggleState "Q1"
  where
    inputI1 = checkInput "I1" ctx
    toggleState output = toggleOutputState output ctx
```

---

## Example 3: Timer ON Delay (TON)  

### Ladder Logic  
```
     I1  --| |----[ TON T1 1000 ]----( Q1 )
```

### Structured Text (ST)
```pascal
IF I1 THEN
    T1(IN := TRUE, PT := T#1s);
END_IF;

IF T1.Q THEN
    Q1 := TRUE;
ELSE
    Q1 := FALSE;
END_IF;
```

### Intermediate Representation (IR)  
```json
{
  "logic": [
    { "type": "IR_XIC", "input": "I1", "output": "T1" },
    { "type": "IR_TON", "timer": "T1", "preset": 1000, "output": "Q1" }
  ]
}
```

### Morley Plutus Script  
```haskell
{-# INLINABLE timerOnDelay #-}
timerOnDelay :: BuiltinData -> BuiltinData -> ScriptContext -> Bool
timerOnDelay datum redeemer ctx = 
  inputI1 && checkTimer "T1" 1000
  where
    inputI1 = checkInput "I1" ctx
    checkTimer timer preset = checkElapsedTime timer preset ctx
```

---

## Example 4: Counter Up (CTU)  

### Ladder Logic  
```
     I1  --| |----[ CTU C1 5 ]----( Q1 )
```

### Structured Text (ST)
```pascal
IF I1 THEN
    C1(CU := TRUE, PV := 5);
END_IF;

IF C1.Q THEN
    Q1 := TRUE;
ELSE
    Q1 := FALSE;
END_IF;
```

### Intermediate Representation (IR)  
```json
{
  "logic": [
    { "type": "IR_XIC", "input": "I1", "output": "C1" },
    { "type": "IR_CTU", "counter": "C1", "preset": 5, "output": "Q1" }
  ]
}
```

### Morley Plutus Script  
```haskell
{-# INLINABLE counterUp #-}
counterUp :: BuiltinData -> BuiltinData -> ScriptContext -> Bool
counterUp datum redeemer ctx = 
  inputI1 && checkCounter "C1" 5
  where
    inputI1 = checkInput "I1" ctx
    checkCounter counter preset = checkCounterValue counter preset ctx
```

---

## Example 5: Arithmetic Addition (ADD)  

### Ladder Logic  
```
     I1  --| |----[ ADD N7:0 N7:1 N7:2 ]----( Q1 )
```

### Structured Text (ST)
```pascal
IF I1 THEN
    N7_2 := N7_0 + N7_1;
END_IF;
```

### Intermediate Representation (IR)  
```json
{
  "logic": [
    { "type": "IR_XIC", "input": "I1", "operation": "ADD", "src1": "N7:0", "src2": "N7:1", "dest": "N7:2" }
  ]
}
```

### Morley Plutus Script  
```haskell
{-# INLINABLE addOperation #-}
addOperation :: BuiltinData -> BuiltinData -> ScriptContext -> Bool
addOperation datum redeemer ctx = 
  inputI1 && addValues "N7:0" "N7:1" "N7:2"
  where
    inputI1 = checkInput "I1" ctx
    addValues src1 src2 dest = addAndStore src1 src2 dest ctx
```

---

## Example 6: Counter Down (CTD)  

### Ladder Logic  
```
     I1  --| |----[ CTD C2 0 ]----( Q2 )
```

### Structured Text (ST)
```pascal
IF I1 THEN
    C2(CD := TRUE, PV := 0);
END_IF;

IF C2.Q THEN
    Q2 := TRUE;
ELSE
    Q2 := FALSE;
END_IF;
```

### Intermediate Representation (IR)  
```json
{
  "logic": [
    { "type": "IR_XIC", "input": "I1", "output": "C2" },
    { "type": "IR_CTD", "counter": "C2", "preset": 0, "output": "Q2" }
  ]
}
```

### Morley Plutus Script  
```haskell
{-# INLINABLE counterDown #-}
counterDown :: BuiltinData -> BuiltinData -> ScriptContext -> Bool
counterDown datum redeemer ctx = 
  inputI1 && checkCounterDown "C2" 0
  where
    inputI1 = checkInput "I1" ctx
    checkCounterDown counter preset = checkCounterDownValue counter preset ctx
```

---

## Example 7: Arithmetic Subtraction (SUB)  

### Ladder Logic  
```
     I1  --| |----[ SUB N7:0 N7:1 N7:2 ]----( Q1 )
```

### Structured Text (ST)
```pascal
IF I1 THEN
    N7_2 := N7_0 - N7_1;
END_IF;
```

### Intermediate Representation (IR)  
```json
{
  "logic": [
    { "type": "IR_XIC", "input": "I1", "operation": "SUB", "src1": "N7:0", "src2": "N7:1", "dest": "N7:2" }
  ]
}
```

### Morley Plutus Script  
```haskell
{-# INLINABLE subOperation #-}
subOperation :: BuiltinData -> BuiltinData -> ScriptContext -> Bool
subOperation datum redeemer ctx = 
  inputI1 && subValues "N7:0" "N7:1" "N7:2"
  where
    inputI1 = checkInput "I1" ctx
    subValues src1 src2 dest = subAndStore src1 src2 dest ctx
```

---

## Example 8: Compare Equal (EQUAL)  

### Ladder Logic  
```
     I1  --| |----[ CMP N7:0 == N7:1 ]----( Q1 )
```

### Structured Text (ST)
```pascal
IF I1 THEN
    IF N7_0 = N7_1 THEN
        Q1 := TRUE;
    ELSE
        Q1 := FALSE;
    END_IF;
END_IF;
```

### Intermediate Representation (IR)  
```json
{
  "logic": [
    { "type": "IR_XIC", "input": "I1", "operation": "EQUAL", "src1": "N7:0", "src2": "N7:1", "output": "Q1" }
  ]
}
```

### Morley Plutus Script  
```haskell
{-# INLINABLE compareEqual #-}
compareEqual :: BuiltinData -> BuiltinData -> ScriptContext -> Bool
compareEqual datum redeemer ctx = 
  inputI1 && compareValues "N7:0" "N7:1" "EQUAL" "Q1"
  where
    inputI1 = checkInput "I1" ctx
    compareValues src1 src2 op output = compareAndSet src1 src2 op output ctx
```

---

## Example 9: State Machine (Sequential Operations)  

### Ladder Logic  
```
     I1  --| |----[ TON T3 500 ]----( Q3 )
     Q3  --| |----[ TON T4 1000 ]----( Q4 )
     Q4  --| |------( Q5 )
```

### Structured Text (ST)
```pascal
IF I1 THEN
    T3(IN := TRUE, PT := T#500ms);
END_IF;

IF T3.Q THEN
    T4(IN := TRUE, PT := T#1s);
END_IF;

IF T4.Q THEN
    Q5 := TRUE;
ELSE
    Q5 := FALSE;
END_IF;
```

### Intermediate Representation (IR)  
```json
{
  "logic": [
    { "type": "IR_XIC", "input": "I1", "output": "T3" },
    { "type": "IR_TON", "timer": "T3", "preset": 500, "output": "Q3" },
    { "type": "IR_XIC", "input": "Q3", "output": "T4" },
    { "type": "IR_TON", "timer": "T4", "preset": 1000, "output": "Q4" },
    { "type": "IR_XIC", "input": "Q4", "output": "Q5" }
  ]
}
```

### Morley Plutus Script  
```haskell
{-# INLINABLE stateMachine #-}
stateMachine :: BuiltinData -> BuiltinData -> ScriptContext -> Bool
stateMachine datum redeemer ctx = 
  inputI1 && sequenceTimers ["T3", "T4"] ["Q3", "Q4", "Q5"]
  where
    inputI1 = checkInput "I1" ctx
    sequenceTimers timers outputs = executeSequentialTimers timers outputs ctx
```
---

## Example 10: Industrial Conveyor State Machine with Deeply Nested Logic

### Description
This example represents a highly complex state machine for an industrial conveyor system with:
- Multiple stages and safety interlocks
- Sequential operations with timers and counters
- Arithmetic calculations for inventory and revenue
- Deeply nested conditions with multiple branches
- Complex conditional branches for conveyor speed adjustments

---

## Ladder Logic  
```
     I1  --| |----[ TON T1 1000 ]----( Q1 )  // Safety Check Timer
     Q1  --| |----[ CTU C1 10 ]----( Q2 )    // Count Items on Conveyor
     Q2  --| |----[ ADD N7:0 N7:1 N7:2 ]----( Q3 ) // Inventory Calculation
     Q3  --| |----[ SUB N7:2 N7:3 N7:4 ]----( Q4 ) // Stock Adjustment
     Q4  --| |----[ MUL N7:4 N7:5 N7:6 ]----( Q5 ) // Calculate Revenue
     Q5  --| |----[ DIV N7:6 N7:7 N7:8 ]----( Q6 ) // Profit Margin
     Q6  --| |----[ CMP N7:8 > N7:9 ]----( Q7 )    // Check Profit Threshold
     Q7  --| |----[ TON T2 500 ]----( Q8 )         // Delay for Logging
     Q8  --| |----[ TOF T3 2000 ]----( Q9 )        // Final State
```

---

## Structured Text (ST)
```pascal
IF I1 THEN
    T1(IN := TRUE, PT := T#1s);
END_IF;

IF T1.Q THEN
    C1(CU := TRUE, PV := 10);
END_IF;

IF C1.Q THEN
    N7_2 := N7_0 + N7_1;
    N7_4 := N7_2 - N7_3;
END_IF;

IF N7_4 > 0 THEN
    N7_6 := N7_4 * N7_5;
    N7_8 := N7_6 / N7_7;
END_IF;

IF N7_8 > N7_9 THEN
    T2(IN := TRUE, PT := T#500ms);
END_IF;

IF T2.Q THEN
    T3(IN := TRUE, PT := T#2s);
END_IF;

IF T3.Q THEN
    Q9 := TRUE;
ELSE
    Q9 := FALSE;
END_IF;
```

---

## Intermediate Representation (IR)  
```json
{
  "logic": [
    { "type": "LL_XIC", "input": "I1", "output": "T1" },
    { "type": "LL_TON", "timer": "T1", "preset": 1000, "output": "Q1" },
    { "type": "LL_XIC", "input": "Q1", "output": "C1" },
    { "type": "LL_CTU", "counter": "C1", "preset": 10, "output": "Q2" },

    { "type": "LL_XIC", "input": "Q2", "operation": "LL_ADD", "src1": "N7:0", "src2": "N7:1", "dest": "N7:2" },
    { "type": "LL_XIC", "input": "Q2", "operation": "LL_SUB", "src1": "N7:2", "src2": "N7:3", "dest": "N7:4" },

    { "type": "LL_XIC", "input": "Q4", "operation": "LL_MUL", "src1": "N7:4", "src2": "N7:5", "dest": "N7:6" },
    { "type": "LL_XIC", "input": "Q5", "operation": "LL_DIV", "src1": "N7:6", "src2": "N7:7", "dest": "N7:8" },

    { "type": "LL_XIC", "input": "Q6", "operation": "LL_GRT", "src1": "N7:8", "src2": "N7:9", "output": "Q7" },
    { "type": "LL_XIC", "input": "Q7", "output": "T2" },
    { "type": "LL_TON", "timer": "T2", "preset": 500, "output": "Q8" },

    { "type": "LL_XIC", "input": "Q8", "output": "T3" },
    { "type": "LL_TOF", "timer": "T3", "preset": 2000, "output": "Q9" }
  ]
}
```

---

## Morley Plutus Script  
```haskell
{-# INLINABLE complexNestedLogic #-}
complexNestedLogic :: BuiltinData -> BuiltinData -> ScriptContext -> Bool
complexNestedLogic datum redeemer ctx = traceIfFalse "Nested Condition Failed" $
  stage1 && stage2 && stage3 && stage4 && stage5
  where
    inputI1 = checkInput "I1" ctx
    stage1 = inputI1 && checkTimer "T1" 1000 && checkCounter "C1" 10

    stage2 = checkArithmetic "LL_ADD" "N7:0" "N7:1" "N7:2" &&
             checkArithmetic "LL_SUB" "N7:2" "N7:3" "N7:4"

    stage3 = checkArithmetic "LL_MUL" "N7:4" "N7:5" "N7:6" &&
             checkArithmetic "LL_DIV" "N7:6" "N7:7" "N7:8"

    stage4 = compareValues "N7:8" "N7:9" "LL_GRT" "Q7" &&
             checkTimer "T2" 500

    stage5 = checkTimer "T3" 2000 && checkOutput "Q9"
```
---

## Fun Bonus Example: Programmable Supply Chain with Real-Time Pricing and On-Chain Incentives

### Description
This program represents a futuristic supply chain system that:
- Adjusts material prices dynamically based on real-time market data from an oracle (e.g., copper prices)
- Calculates procurement costs using arithmetic operations
- Verifies delivery and quality metrics on-chain
- Rewards or penalizes suppliers based on performance
- Updates on-chain reputation scores using dynamic incentives
- Uses state machines, nested logic, and advanced function blocks
- Mints tokens for rewards or burns tokens for penalties

### Flow
1. Fetch real-time pricing data using verifiable oracle.
2. Adjust procurement costs dynamically.
3. Verify delivery times and quality on-chain.
4. Automatically reward or penalize suppliers.
5. Update reputation scores on-chain.

---

## Ladder Logic  
```
     O1  --| |----[ ORACLE PRICE_FETCH ]----( P1 )  // Fetch Price from Oracle
     P1  --| |----[ MUL P1 QTY COST ]----( C1 )     // Calculate Procurement Cost
     D1  --| |----[ CMP DELAY > TOLERANCE ]----( P2 ) // Check Delivery Delay
     Q1  --| |----[ CMP QUALITY < THRESHOLD ]----( P3 ) // Check Quality
     P2  --| |----[ PENALTY LATE ]----( P4 )         // Apply Late Penalty
     P3  --| |----[ PENALTY LOW_QUALITY ]----( P5 )  // Apply Quality Penalty
     P4  --| |----[ BURN TOKENS PENALTY ]----( P6 )  // Burn Tokens for Penalty
     P5  --| |----[ BURN TOKENS PENALTY ]----( P7 )  // Burn Tokens for Penalty
     P6  --| |------( UPDATE REPUTATION )            // Update On-Chain Reputation
     P7  --| |------( UPDATE REPUTATION )            // Update On-Chain Reputation
     P1  --|/|----[ REWARD ON_TIME ]----( R1 )       // Reward for On-Time Delivery
     R1  --| |----[ MINT TOKENS REWARD ]----( R2 )   // Mint Tokens for Reward
     R2  --| |------( UPDATE REPUTATION )            // Update On-Chain Reputation
```

---

## Structured Text (ST)
```pascal
// Stage 1: Fetch Real-Time Price
IF O1 THEN
    P1 := ORACLE_PRICE_FETCH();
END_IF;

// Stage 2: Calculate Procurement Cost
C1 := P1 * QTY;

// Stage 3: Check Delivery Delay
IF DELAY > TOLERANCE THEN
    PENALTY := TRUE;
    TOKENS := BURN(PENALTY);
    UPDATE(REPUTATION);
ELSE
    REWARD := TRUE;
    TOKENS := MINT(REWARD);
    UPDATE(REPUTATION);
END_IF;

// Stage 4: Check Quality
IF QUALITY < THRESHOLD THEN
    PENALTY := TRUE;
    TOKENS := BURN(PENALTY);
    UPDATE(REPUTATION);
END_IF;
```

---

## Intermediate Representation (IR)  
```json
{
  "logic": [
    { "type": "LL_XIC", "input": "O1", "operation": "LL_ORACLE", "action": "PRICE_FETCH", "output": "P1" },
    { "type": "LL_XIC", "input": "P1", "operation": "LL_MUL", "src1": "P1", "src2": "QTY", "dest": "C1" },

    { "type": "LL_XIC", "input": "D1", "operation": "LL_CMP", "src1": "DELAY", "src2": "TOLERANCE", "cmp": "GT", "output": "P2" },
    { "type": "LL_XIC", "input": "Q1", "operation": "LL_CMP", "src1": "QUALITY", "src2": "THRESHOLD", "cmp": "LT", "output": "P3" },

    { "type": "LL_XIC", "input": "P2", "operation": "LL_PENALTY", "action": "LATE", "output": "P4" },
    { "type": "LL_XIC", "input": "P3", "operation": "LL_PENALTY", "action": "LOW_QUALITY", "output": "P5" },

    { "type": "LL_XIC", "input": "P4", "operation": "LL_BURN", "token": "PENALTY", "output": "P6" },
    { "type": "LL_XIC", "input": "P5", "operation": "LL_BURN", "token": "PENALTY", "output": "P7" },

    { "type": "LL_XIC", "input": "P6", "operation": "LL_UPDATE", "action": "REPUTATION" },
    { "type": "LL_XIC", "input": "P7", "operation": "LL_UPDATE", "action": "REPUTATION" },

    { "type": "LL_XIO", "input": "P1", "operation": "LL_REWARD", "action": "ON_TIME", "output": "R1" },
    { "type": "LL_XIC", "input": "R1", "operation": "LL_MINT", "token": "REWARD", "output": "R2" },

    { "type": "LL_XIC", "input": "R2", "operation": "LL_UPDATE", "action": "REPUTATION" }
  ]
}
```

---

## Morley Plutus Script  
```haskell
{-# INLINABLE dynamicSupplyChain #-}
dynamicSupplyChain :: BuiltinData -> BuiltinData -> ScriptContext -> Bool
dynamicSupplyChain datum redeemer ctx = traceIfFalse "Supply Chain Logic Failed" $
  stage1 && stage2 && stage3 && stage4 && stage5
  where
    inputO1 = checkInput "O1" ctx
    stage1 = inputO1 && fetchOraclePrice "PRICE_FETCH" "P1"

    stage2 = checkArithmetic "LL_MUL" "P1" "QTY" "C1"

    stage3 = (compareValues "DELAY" "TOLERANCE" "LL_GRT" && burnToken "PENALTY") ||
             (compareValues "QUALITY" "THRESHOLD" "LL_LES" && burnToken "PENALTY") ||
             (not (compareValues "DELAY" "TOLERANCE" "LL_GRT") && mintToken "REWARD")

    stage4 = checkOutput "R2" && updateReputation "REPUTATION"
    stage5 = checkOutput "P6" || checkOutput "P7"
```
