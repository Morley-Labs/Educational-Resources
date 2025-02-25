
## 10 Basic Ladder Logic Programs with Structured Text, IR, and Morley Plutus Scripts

### Example 1: Start-Stop Circuit (Basic Latching Logic)  

#### Ladder Logic  
```
     I1  --| |------( Q1 )   // Start Button (Normally Open Contact)
     I2  --|/|------( Q1 )   // Stop Button (Normally Closed Contact)
     Q1  --| |------( Q1 )   // Latching to keep Motor ON
```

#### Structured Text (ST)
```pascal
IF I1 THEN
    Q1 := TRUE;
END_IF;

IF I2 THEN
    Q1 := FALSE;
END_IF;
```

#### Intermediate Representation (IR)  
```json
{
  "logic": [
    { "type": "IR_XIC", "input": "I1", "output": "Q1" },
    { "type": "IR_XIO", "input": "I2", "output": "Q1" },
    { "type": "IR_XIC", "input": "Q1", "output": "Q1" }
  ]
}
```

#### Morley Plutus Script  
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

### Example 2: Timer ON Delay (TON)  

#### Ladder Logic  
```
     I1  --| |----[ TON T1 1000 ]----( Q1 )
```

#### Structured Text (ST)
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

#### Intermediate Representation (IR)  
```json
{
  "logic": [
    { "type": "IR_XIC", "input": "I1", "output": "T1" },
    { "type": "IR_TON", "timer": "T1", "preset": 1000, "output": "Q1" }
  ]
}
```

#### Morley Plutus Script  
```haskell
{-# INLINABLE timerOnDelay #-}
timerOnDelay :: BuiltinData -> BuiltinData -> ScriptContext -> Bool
timerOnDelay datum redeemer ctx = 
  inputI1 && checkTimer "T1" 1000
  where
    inputI1 = checkInput "I1" ctx
    checkTimer timer preset = checkElapsedTime timer preset ctx
```

### Example 3: Counter Up (CTU)  

#### Ladder Logic  
```
     I1  --| |----[ CTU C1 5 ]----( Q1 )
```

#### Structured Text (ST)
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

#### Intermediate Representation (IR)  
```json
{
  "logic": [
    { "type": "IR_XIC", "input": "I1", "output": "C1" },
    { "type": "IR_CTU", "counter": "C1", "preset": 5, "output": "Q1" }
  ]
}
```

#### Morley Plutus Script  
```haskell
{-# INLINABLE counterUp #-}
counterUp :: BuiltinData -> BuiltinData -> ScriptContext -> Bool
counterUp datum redeemer ctx = 
  inputI1 && checkCounter "C1" 5
  where
    inputI1 = checkInput "I1" ctx
    checkCounter counter preset = checkCounterValue counter preset ctx
```

