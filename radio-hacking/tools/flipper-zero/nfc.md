# NFC

The flipper can read and emulate RFID and NFC cards, making it useful for proximity-based systems.

## Example Usage: Clone a Mifare Classic Card

#### 1. Go to NFC Menu:

* From the main menu, select NFC.
* This is where you can read, save, emulate, and write NFC cards.

#### 2. Read the Mifare Classic Card:

* Place the Mifare Classic card (target card) on the back of the Flipper Zero, where the NFC antenna is located.
* In the NFC menu, select Read to start reading the card.
* If the card is readable, the Flipper Zero will display the details of the card, including the UID (Unique Identifier).

{% tabs %}
{% tab title="Mifare Classic" %}
* Flipper Zero can read and save data from the following cards:
  * MIFARE Classic 1K
  * MIFARE Classic 4K
  * MIFARE Classic Mini
* To read data stored in sectors, Flipper Zero needs to find:
  * 32 keys for 16 sectors (MIFARE Classic 1K)
  * 80 keys for 40 sectors (MIFARE Classic 4K)
  * 10 keys for 5 sectors (MIFARE Classic Mini)
* Flipper Zero uses keys from the System dictionary to find these keys.
* You can add your keys to the User dictionary by navigating to:
  * Main Menu -> NFC -> Extra Actions -> MIFARE Classic Keys.



If the keys are found in the dictionary the card can now be completley be emulated:

<figure><img src="../../../.gitbook/assets/image (29).png" alt="" width="319"><figcaption><p>All keys are read</p></figcaption></figure>

If not, all keys are found we can try to get the missing keys from the card reader, like described here: [https://docs.flipper.net/nfc/read#fGAwL](https://docs.flipper.net/nfc/read#fGAwL). Perform the following steps:

1. Read the NFC card and save it with your Flipper Zero.&#x20;
2. In "Main Menu -> NFC -> Saved -> Name of the saved card" select "Extract MF Keys" which will make the Flipper emulate this card for the MFKey32 attack.
3. Tap  your flipper around 10 times onto the corresponding reader of the card, which will collect nonces from the reader
4. Use the MFKey32 app on your flipper or mobile phone(inside flipper app) to try to recover missing keys.&#x20;
5. read the NFC card again and hope the missing keys are now found
6. if yes you can emulate the card now

<figure><img src="../../../.gitbook/assets/image (28).png" alt="" width="505"><figcaption><p>Sectors needs to be unlocked</p></figcaption></figure>
{% endtab %}

{% tab title="NFC cards type V" %}
Todo
{% endtab %}

{% tab title="NFC cards type F" %}
Todo
{% endtab %}
{% endtabs %}

#### 3. Emulate card

If all keys and sectors could be recovered, we can now use the flipper to emulate the card and perform the same action the card itself could do.

## Resources

*[NFC - Flipper Zero Documentation](https://docs.flipper.net/nfc)
