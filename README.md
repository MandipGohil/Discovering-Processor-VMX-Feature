# Discovering-Processor-VMX-Feature

# Discover VMX features present in your processor by writing a Linux kernel module that queries these featurs.

# Prerequisites
• You will need a machine capable of running Linux, with VMX virtualization features exposed. You
may be able to do this inside a VM, or maybe not, depending on your hardware and software
configuration.

# At a high level, you will need to perform the following:
• Configure a Linux machine, either VM based or on real hardware. You may use any Linux
distribution you wish.
• Download and build the Linux kernel source code
• Create a new kernel module with the assignment functionality
• Load (insert) the new module
• Verify proper output in the system message log.

# Functionality to Implemented
You will need to perform the following in your module’s main code:
• Determine if your CPU supports VMX true controls
• Based on the above, read various MSRs to ascertain support capabilities/features
◦ Entry / Exit / Procbased / Secondary Procbased / Pinbased controls
• For each group of controls above, interpret and output the

# To determine if true controls are available:
• Read the IA32_VMX_BASIC MSR
• Check bit 55 – if set, true controls are available.

# To determine if secondary procbased controls are available:
• Check the ability to set “Activate Secondary Controls” control in the primary procbased controls
◦ There are no “true secondary procbased controls”, so there is only one MSR to read if the
CPU supports secondary controls.

# The table below provides some MSRs that may be of interest to you.
# MSR Name MSR -->Index -->Notes

IA32_VMX_BASIC --> 0x480 -->Use this to determine true controls capability
(bit 55)

IA32_VMX_PINBASED_CTLS -->0x481 -->Use this MSR for pinbased controls if no true
controls capability

IA32_VMX_PROCBASED_CTLS -->0x482 -->Use this MSR for procbased controls if no true
controls capability

IA32_VMX_PROCBASED_CTLS2 -->0x48B -->Use this MSR for secondary procbased
controls, if available

IA32_VMX_EXIT_CTLS -->0x483 -->Use this MSR for exit controls if no true
controls capability

IA32_VMX_ENTRY_CTLS -->0x484 -->Use this MSR for entry controls if no true
controls capability

IA32_VMX_TRUE_PINBASED_CTLS -->0x48D -->Use this MSR for pinbased controls if CPU
supports true controls

IA32_VMX_TRUE_PROCBASED_CTLS -->0x48E -->Use this MSR for procbased controls if CPU
supports true controls

IA32_VMX_TRUE_EXIT_CTLS -->0x48F -->Use this MSR for exit controls if CPU
supports true controls

IA32_TRUE_ENTRY_CTLS -->0x490 -->Use this MSR for entry controls if CPU
supports true controls
