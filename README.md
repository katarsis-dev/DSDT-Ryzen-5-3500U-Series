# DSDT-Ryzen-5-3500U-Series

## 1. Keyboard Builtin Not Working properly **(Fixed)**

### Option Solution:
* **Using External Keyboard**
* **Add `pnpacpi=off` to `GRUB_CMDLINE_LINUX_DEFAULT` inside `/etc/default/grub`**
    * *(Easy but Not Recommended, for long term purpose, most likely will turn off power management for input output hardware)*
    * > i still study about these, whats the trade off, and whats the benefit clearly
* **Patch DSDT** *(Kinda hard but recommended, as long as you don't touch anything other than the keyboard on the code, it "should" be safe, and if theres error on code,it will go kernel panic)*
    1.  Get your acpi that u using, get the `dsdt.dsl`, go find on google how to do it.
    2.  After that, open the file with vscode, find `"PNP0303"`, make sure code on top of that is `Device(PS2K)` (it identifer as keyboard).
    3.  It most likely not working cause `"Edge, ActiveLow, Share"`. Go change whit `"Edge, ActiveHigh, Share"`.
    4.  Make sure add some 1 letter on definition block.
    5.  Then yep, compile into acpi again and use it.

---

## 2. GPU Memory Clock Lock in some of frequency **(Not Fixed)**
# Its not fixed its just pure driver bug, idk why but in my experiment the trigger that make my memory clock full and stuck on some frequency its because im using brave browser, idk is it cause brave itself, or its just cause its chromium base application
# next time i will try using different driver , changing kernel for me not changing anything
*(Most likely problem on `amdgpu` driver, so i cant do anything for now)*

### What have I tried?
* Add paremeter `acpi_osi="Windows 2015"` on `GRUB_CMDLINE_LINUX_DEFAULT` (still not working).
* Edit dsdt patch on `Method (OSTP, 0, NotSerialized)`, still not changing anything.

---

> For the next part maybe i will try more to edit on acpi table area, cause i dont want to go far and i dont want to deal with bios patching / editing cause its too risky.
