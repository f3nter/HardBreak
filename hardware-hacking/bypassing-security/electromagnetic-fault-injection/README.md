# Electromagnetic Fault Injection

## **Theory**

Electromagnetic Fault Injection (EMFI) is a type of fault injection attack where an attacker manipulates the current flowing inside a CPU with the help of electromagnetic induction. With the operations inside of an Integrated Circuit (IC) being controlled by the current flowing between and controlling the transistors, manipulating this current might result in faults being injected. EMFI is based on the physical principle of 'Electromagnetic Induction', which in itself is described through Faraday's law of induction. The law can be used to show how an electric circuit will produce a force known as electromagnetic induction when interacting with a magnetic field. In general, this means that by using magnetic fields, it is possible to induct a current into an electrical circuit.

Manipulating the current flowing inside the IC poses a chance of changing certain registers or states and therefore allowing an attacker to tamper with the system. By sending a short, but strong current through a coil, it creates a magnetic field around said coil. Placing the coil above a chip then ideally induces a voltage in the IC of that chip. This potentially disrupts the normal execution flow of the processor or microcontroller. Based on the location and timing of the pulse, it allows an attacker to possibly induce faults and trigger unintended behaviour in the system.

The effectivness of EMFI depends on the timing and duration of the sent pulse, the strenght of the magnetic field (which is related to the current running through the coil, and the parameters of the coil itself) and the location of the coil next to the chip.

In contrast to other fault injection techniques, EMFI allows for glitching without necessarily having to tamper with the board itself. Other types of fault injection often require desoldering capacitors or decapsulating processors. With the coil being simply placed on top of the processor, manipulating the hardware of the board being attacked is usually not required.

## Usage

* A common scenario where EMFI can be applied is in bypassing secure boot mechanisms of microcontrollers.
  * The attacker sets up an EMFI device (like a PicoEMP or ChipShouter), placing a coil above the processor.
  * Using this equipment, an attacker sends a short pulse of power through the attached coil. The magnetic field around the coil induces a current in the IC of the processor.
  * By timing the glitches precisely, the attacker migth disrupt verification routines, causing the system to mistakenly accept unauthorized firmware or bypass security checks entirely.
* For example, an attacker targeting a microcontroller running a protected bootloader might attempt EMFI glitching to bypass code signing checks:
  * First, they monitor the power consumption patterns of the device during the boot process to identify the moment when security checks occur.
  * Next, they configure the EMFI device to send a pulse at the timing of the check. Having a precise timing and the exact location where on the chip the check is taking place will increase the chance of the induced current being able to manipulate the system in a way where it, for example, skips the check entirely.
  * If successful, the security check fails, and the system proceeds with unauthorized code execution.

## Resources

*[Electromagnetic Fault Injection](https://circuitcellar.com/research-design-hub/electromagnetic-fault-injection/)
*[A Compact Electromagnetic Fault Injection Setup](https://www.ledger.com/blog/compact-em)
*[Electromagnetic fault injection: the curse of flip-flops](https://hal.science/lirmm-01430913/)

## Page Contributors

* [https://github.com/Whit3rose](https://github.com/Whit3rose)
