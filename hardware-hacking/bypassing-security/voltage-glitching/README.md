# Voltage Glitching

## **Theory**

Voltage glitching is a type of fault injection attack where an attacker manipulates the power supply voltage of a system to induce errors in its operations. It exploits the vulnerability of electronic circuits, particularly when they are under abnormal operating conditions. By temporarily lowering or increasing the supply voltage at critical moments, attackers can disrupt the normal execution flow of a processor or microcontroller. This can lead to skipping instructions, bypassing security checks, or triggering unintended behavior in the system. Voltage glitching is especially effective in embedded systems, as they often lack sophisticated protection mechanisms against such physical attacks.

The effectiveness of voltage glitching depends on the timing (offset) and precision of the glitch. Well-timed glitches can cause subtle and hard-to-detect faults that compromise system integrity. These attacks often require physical access to the device, as the power supply needs to be manipulated directly.

## Usage

* A common scenario where voltage glitching can be applied is in bypassing secure boot mechanisms of microcontrollers or smart cards.
  * The attacker connects a controllable power supply to the target device's power input.
  * Using specialized equipment, the attacker introduces short, rapid voltage drops during critical phases, such as the authentication process or when the secure bootloader is verifying firmware.
  * By timing the glitches precisely, the attacker can disrupt verification routines, causing the system to mistakenly accept unauthorized firmware or bypass security checks entirely.
* For example, an attacker targeting a microcontroller running a protected bootloader might attempt voltage glitching to bypass code signing checks:
  * First, they monitor the power consumption patterns of the device during the boot process to identify the moment when security checks occur.
  * Next, they configure the voltage glitcher to induce a power drop at the identified time window.
  * If successful, the security check fails, and the system proceeds with unauthorized code execution.&#x20;

Always try to desolder the target chip from the actual PCB, as components like capacitors will weaken the glitch:

1. An optimal voltage glitch without a target connected can be seen in this figure, looks like this:

<figure><img src="../../../.gitbook/assets/image (59).png" alt=""><figcaption><p>An optimal voltage glitch without a target connected can be seen in this figure</p></figcaption></figure>

2. If you connect the whole PCB, it may look like this. (no sharp edges)

<figure><img src="../../../.gitbook/assets/image (60).png" alt=""><figcaption><p>1<br></p></figcaption></figure>

3. Glitch (blue line) with soldered off target chip, looks more like the optimal glitch.

<figure><img src="../../../.gitbook/assets/image (21).png" alt=""><figcaption><p>best glitch<br></p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (22).png" alt=""><figcaption><p>Desoldered chip</p></figcaption></figure>

## Resources

* [Glitching An ATMega328P Has Never Been Simpler](https://hackaday.com/2024/06/03/glitching-an-atmega328p-has-never-been-simpler/)
* [Episode 4 – Power Glitch Attack](https://www.ledger.com/academy/series/enter-the-donjon/episode-4-power-glitch-attack)
