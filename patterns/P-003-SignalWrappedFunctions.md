# 🧠🌀 Signal-Wrapped Functions

## A Pattern for Sovereign-Compliant, Context-Preserving Execution

### 📅 Date: 2025-05-14  
### 🏷️ Version: 1.0

---

### 🔍 Summary

**Signal-Wrapped Functions** is a design pattern in which **every function receives and returns a Signal object**, ensuring full traceability, recursive introspection, and memory-safe mutation within a sovereign execution context.

This pattern enforces **contextual integrity** — allowing every function to operate within the lineage, environment, and purpose embedded in the incoming signal.

---

### 🔧 Core Principles

- **All inputs and outputs are Signals**  
- **No function returns raw values** — only a transformed `Signal`
- **The Signal carries all execution state**, including `.Jacket`, `.Pointer`, `.Result`, `.TraceID`
- **Failure and success paths are merged via signal diagnostics**, not conditionals

---

### 📐 Function Signature Structure

```powershell
function <Verb-Noun> {
    param ([ConductionSignal]$Signal)

    $Signal = [Signal]::Start("FunctionName") | Select-Object -Last 1
    ...
    return $Signal
}
```

> *All downstream logic must also use signal calls (e.g., `Resolve-PathFromDictionary`, `Add-PathToDictionary`) for compliance.*

---

### 🧪 Example

```powershell
function Compute-DoubledValue {
    param ([ConductionSignal]$Signal)

    $Signal = [Signal]::Start("Compute-DoubledValue") | Select-Object -Last 1

    $valueSignal = Resolve-PathFromDictionary -Dictionary $Signal -Path "$.Input.Number" | Select-Object -Last 1
    if ($Signal.MergeSignalAndVerifyFailure($valueSignal)) {
        return $Signal.LogCritical("❌ Missing input: $.Input.Number")
    }

    $value = $valueSignal.GetResult()
    $Signal = Add-PathToDictionary -Signal $Signal -Path "$.Output.Doubled" -Value ($value * 2) | Select-Object -Last 1
    return $Signal
}
```

---

### 🧱 Benefits

- ✅ Consistent lineage across recursive calls  
- ✅ Enables sovereign debugging and recovery  
- ✅ Prevents silent errors or untracked mutation  
- ✅ Easy to plug into Graph-based or Plan-based execution engines  
- ✅ Abstracts logic away from imperative control flow

---

### 🚫 Anti-Patterns

- Returning primitive or object types (`int`, `hashtable`, etc.)  
- Using `$obj.Property = value` instead of `Add-PathToDictionary`  
- Directly modifying `$Signal.Result` without merge semantics  
- Skipping `.Start()` wrapper at function entry

---

### 🧩 Integration Patterns

- **Signal-Oriented Execution Model**: The overarching execution framework  
- **Signal-Based Execution**: End-to-end control flow through Signal chains  
- **Graph-Driven Function Dispatch**: Functions embedded in DAGs via signal wiring  
- **Hydration Condensers**: Declarative invocation based on Signal-defined intent

---

### 🧾 Canon Reference

**Pattern Name**: Signal-Wrapped Functions  
**Pattern Class**: Sovereign Execution Flow  
**Glyph**: 🧠🌀  
**Version**: 1.0  
**Date**: 2025-05-14  
**Originators**: Shadow PhanTom, Neural Alchemist  
**First Use**: SDA Runtime Core, 2025
