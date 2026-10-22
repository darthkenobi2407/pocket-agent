# Pocket Agent  system architecture

## 1. objectives:

### 2.1 functional objectives
>>it should be able to interpret natural language user requsts
>>convert these requests into action proposals
>>validate the proposals against the defined actin scheme 
>>display the propsed action and relevant paramters
>>require user approval for executing these actions
>>communicate with the companion application on the phone
>>execute only supported and authorzed actions
>>record action status and recover from failures safely


### 2.2 engineering objectives

>>use the Radxa cm5 w/ 16gb ram as the inital compute baseline
>>prefer handling requests locally than using external ai 
>>use deterministic logic for authorization and execution 
>>keep clear boundaires between the model and privelleged operations 
>>design should be small compact handheld enclosure 


## 2. Hardware Architecture

### 2.1 compute module

** the first selected baseline is the  Radxa CM5**

The Radxa CM5 is based on the Rockchip RK3588S2 and it integrates the CPU, GPU, NPU, memory, power-management circuitry, and onboard storage.

The module physical mesaurements are approximately 55 × 40 mm which makes it a compact candidate for the device.

Key specifications:

- CPU: four cortex-A76 cores and four cortex-A55 cores
- NPU: advertised peak capability of up to 6 TOPS
- Memory: lpddr4x
- Storage: Onboard eMMC configurations vary by SKU usually 
- Operating system: debian based Radxa OS is the initial software baseline


Reference: https://docs.radxa.com/en/som/cm/cm5

### 2.2 memory

**initial memory requirement is 16 GB LPDDR4X RAM**

Memory has to  accommodate the OS, background services, model weights, inference runtime, context & KV cache, UI, and action processing components

The usable memory for inference will mostly be lower than the installed capacity because the operating system and other processes also consume ram

### 2.3 storage

The exact storage capacity isnt decided yet but storage has to accomomdate the OS , system updates , application boundaries and dependencies ,  model files and the tokenizer assets , config and policy files , logs and diagonstic info , temp files and model loading overhead

The storage decision should account for model size, available eMMC configurations, expected logging volume, and update requirements.

Storage capacity must not be confused with working memory: model files stored on eMMC still need to be loaded into memory for inference.

### 3.4 carrier board

still building , will lyk


### 3.5 display and physical controls



### 3.6 Physical constraints


## 4. Operating System and Software Stack

### 4.1 Operating system


### 4.2 Software components


### 4.3 Process boundaries


## 5. AI Inference Architecture

### 5.1 Local-first inference

### 5.2 Initial model candidate

### 5.3 Inference runtime


### 5.4 Output contract


## 6. Action Execution Architecture

### 6.1 Separation of responsibilities


### 6.2 Deterministic policy engine


### 6.3 Approval binding

A
### 6.4 Limited execution scope

## 7. Phone Companion and External Services

### 7.1 Companion application

### 7.2 External service adapters


### 7.3 Credentials


## 8. Communication and Authorization

### 8.1 Communication channel

### 8.2 Message validation


### 8.3 Replay protection and revocation


## 9. Action State and Failure Handling


### 9.1 Failure conditions

### 9.2 Uncertain execution outcomes


## 10. State, Logging, and Recovery


## 11. Performance and Power Evaluation

### 11.1 Memory measurements


### 11.2 Power and thermal measurements


## 12. Development and Verification Plan

### Phase 1 — Compute validation

- Confirm the exact Radxa CM5 SKU with 16 GB RAM.
- Select a compatible development IO board.
- Boot the selected operating-system image.
- Record the OS, kernel, and relevant firmware versions.
- Confirm access to the required compute and peripheral interfaces.

### Phase 2 — Inference benchmark

- Install a compatible inference runtime.
- Select a small quantized model for initial evaluation.
- Verify model compatibility and output correctness.
- Measure latency, peak RAM, power, and temperature.
- Determine whether the selected runtime and model meet the initial requirements.

### Phase 3 — Proposal pipeline

- Implement the structured action schema.
- Build strict parsing and validation.
- Add deterministic policy checks.
- Implement proposal identifiers and approval binding.
- Test malformed, unsupported, and ambiguous proposals.

### Phase 4 — Approval interface

- Display the exact action and parameters.
- Implement approve, reject, and cancel interactions.
- Ensure changes invalidate earlier approval.
- Test timeout and interrupted-session behavior.

### Phase 5 — Phone integration

- Select the phone platform and communication transport.
- Implement authenticated pairing and message validation.
- Build one narrowly scoped service adapter.
- Test authorization, replay resistance, disconnection, and duplicate requests.

### Phase 6 — Reliability testing

- Test process crashes and device restarts.
- Test uncertain execution outcomes.
- Verify that unsupported operations cannot execute.
- Measure end-to-end latency.
- Record unresolved failures and security limitations.

### Phase 7 — Custom hardware

- Finalize display, controls, and connectivity requirements.
- Estimate battery and thermal requirements from measurements.
- Design the carrier PCB.
- Develop the enclosure around actual component dimensions.
- Validate the integrated device before claiming final performance.

## 13. Open Engineering Decisions

## 14. References

- Radxa CM5 documentation: https://docs.radxa.com/en/som/cm/cm5
- Radxa CM5 product page: https://radxa.com/products/cm/cm5/
- Radxa OS documentation: https://docs.radxa.com/en/som/cm/cm5/download
- Radxa AI application documentation: https://docs.radxa.com/en/som/cm/cm5/radxa-os/app-dev/ai
- RKLLM documentation: https://docs.radxa.com/en/rock5/rock5c/app-development/ai/rkllm-install

Documentation and configuration availability may vary by hardware revision, SKU, and software release. Verify compatibility against the exact hardware and software being used.

