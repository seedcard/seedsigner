# seedsigner tools

**Feature Proposal: Passphrase QR Code Creation**

**Objective:**  
Enhance the functionality of SeedSigner by introducing a "Passphrase QR Creation" feature within the 'Tools' menu. This feature will allow users to generate a QR code from their passphrase text, providing an additional layer of convenience and usability.

---

### **Feature Details**

**Overview:**  
The "Passphrase QR Creation" feature will enable users to input their passphrase and generate a scannable QR code directly on the device. This can then be used to engrave the qr code on a secure steel plate  for storage or to scan for quick re-entry into another device when needed. 

**Key Components:**  
1. **Input Text Field:**  
   - Allow users to manually enter their passphrase via the SeedSigner device's input interface.
   
2. **QR Code Generation:**  
   - Use Python libraries such as `qrcode` or equivalent to encode the input text into a QR code.
   - Display the generated QR code on the device screen.

3. **Display Options:**  
   - Offer an option to enlarge the QR code for better visibility on the device screen.
   - Include a button for the user to return to the Tools menu after viewing.

---

### **Implementation Steps**

1. **Passphrase Input Handling:**  
   - Create a new menu item under 'Tools' labeled "Passphrase QR Creation."
   - Use existing input interfaces to capture user input for the passphrase.

2. **QR Code Generation Logic:**  
   - Integrate a QR code generation library (e.g., `qrcode`) into the project.
   - Generate a QR code from the input string and prepare it for rendering.

3. **Rendering the QR Code:**  
   - Use the device's screen interface to display the QR code.
   - Ensure the QR code is scannable and clearly rendered.

4. **Testing and Validation:**  
   - Validate the QR code generation and display process with various passphrase lengths and characters.
   - Ensure proper error handling for edge cases (e.g., overly long passphrases).

---

### **Code Snippet Example**

```python
import qrcode
from PIL import Image
from io import BytesIO

def generate_passphrase_qr(passphrase):
    """
    Generate a QR code from the given passphrase.
    
    Args:
        passphrase (str): The passphrase to encode.

    Returns:
        Image: The generated QR code as a PIL image.
    """
    try:
        # Create QR Code
        qr = qrcode.QRCode(
            version=1,
            error_correction=qrcode.constants.ERROR_CORRECT_L,
            box_size=10,
            border=4,
        )
        qr.add_data(passphrase)
        qr.make(fit=True)

        # Generate image
        img = qr.make_image(fill_color="black", back_color="white")
        return img
    except Exception as e:
        print(f"Error generating QR code: {e}")
        return None

# Example usage
if __name__ == "__main__":
    passphrase = input("Enter your passphrase: ")
    qr_image = generate_passphrase_qr(passphrase)
    if qr_image:
        qr_image.show()
```

---

### **Benefits of This Feature**
1. **Convenience:** Enables quick retrieval and usage of passphrases without manual entry.
2. **Security:** Reduces the likelihood of typographical errors during passphrase re-entry.
3. **Enhanced Usability:** Aligns with SeedSigner's goal to simplify Bitcoin wallet management for users.

**Estimated Development Time:** TBA

**Dependencies:**  
- Python libraries: `qrcode`, `Pillow`.  
- Compatibility with the SeedSigner device's screen and input/output interface.

---

Let me know if you'd like further refinements or details!
