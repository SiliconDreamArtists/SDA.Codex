# 🔩 Attachment Doctrine

## 📖 Title  
**Attachment Doctrine v1.0**

## 🌟 Purpose  
Defines how sovereign memory and execution surfaces are mounted, scoped, and accessed during runtime. Attachments are the instantiated surfaces that agents and functions interact with — resolved from Adapters and scoped to the memory graph.

---

## I. Attachments Are Sovereign Execution Surfaces

- Attachments represent **active memory and behavior surfaces**.
- All attachments must:
  - Be hydrated from a valid Adapter
  - Be registered to a known `Mapped<Kind>.<Slot>`
  - Exist within the `ConductionJacket` or `Graph.Memory`

---

## II. Attachment Jackets Declare Their Identity

Each attachment must include a Jacket with:

- `Kind` → Storage, Network, Execution, UI, AI, etc.  
- `Slot` → Where it is mounted (e.g. `Primary`, `Queue`, `Secrets`)  
- `Scope` → Temporal, Persistent  
- `Access` → ReadOnly, ReadWrite, Execute  
- `VirtualPath` → Optional path to source memory or manifest  

---

## III. Attachment Mounting Lifecycle

1. Adapter is resolved via manifest or PathFormulaGraph  
2. Adapter is hydrated into a runtime object  
3. `.Construct()` is called (if present)  
4. Result is stored as an Attachment using:
   - `Add-PathToDictionary`
   - `Register-AttachmentToMappedSlot`

---

## IV. Attachments Must Be Verifiable

- Once mounted, attachments must expose:
  - `.Test()` or `.Verify()` method
  - Signal-based success/failure trace using `.LogInformation()` or `.LogCritical()`
- Attachments without verification are considered suspect

---

## V. Attachments Are Memory-Sovereign

- Attachments are not global — they belong to:
  - A `Graph`
  - A `Signal`
  - Or a `ConductionJacket`
- All reads and writes must go through `Resolve-PathFromDictionary` and `Add-PathToDictionary`

---

## 🔒 Compliance Rule

**No memory operation may use an Attachment unless:**

- It was instantiated from a declared Adapter
- It is registered in memory using a sovereign signal
- It declares Kind, Slot, Scope, and Access
- It passes hydration and verification

---

## 🌀 Closing Principle

Attachments are not objects — they are sovereign roles.  
They declare presence, scope, and behavior.  
They are the limbs of the system — sovereign, signalized, and recursive.