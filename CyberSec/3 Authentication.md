- Memory cards
- Barcodes
- Magnetic stripe cards
- Smart cards
	- Contact
	- Contactless
- RFIDs

### Authentication via Barcodes
Boarding passes, which are created at flight check-in and scanned before boarding.
In most applications, however, barcodes provide convenience but not security.
- Since barcodes are simply images, they are extremely easy to duplicate
### Magnetic Stripe Cards
Plastic card with a magnetic stripe containing personalized information about the card holder.
- The first track of a magnetic stripe card contains the cardholder's full name in addition to an account number, format information, and other data.
- The second track may contain the account number, expiration date, information about the issuing bank, data specifying the exact format of the track, and other discretionary data

>[!tip] Security
>One vulnerability of the magnetic stripe medium is that it is easy to read and reproduce.
>Magnetic stripe readers can be purchased at relatively low cost, allowing attackers to read information off cards. When couples with a magnetic stripe writer, which is only a little more expensive, an attacker can easily clone existing cards. so many uses require card holders to enter a PIN to use their cards.

### Smart tokens
Physical charateristics:
- include an embedded microprocessor
- a smart token that looks like a bank card
User interface:
- Manual interfaces include a keypad and display for human/token interaction
- Electronic interface
A smart card or other token requires an electronic interface to communicate with a compatible reader/writer.
- contact and contactless interfaces
Authentication protocol:
- classified into three categories:
	- static
	- dynamic password generator
	- challenge-response
### Smart Cards
Most important category of smart token 
- has the appearance of a credit card
- has an electronic interface
- may use any of the smart token protocols
Contain an entire microprocessor with 
- processor 
- memory
- I/O ports
Typically include three types of memory:
- Read-only memory (ROM)
	- stores data that does not change during the card's life
- Electrically erasable programmable ROM (EEPROM)
	- hold application data and programs
- Random access memory (RAM)
	- holds temporary data generated when applications are executed

>[!note] Electronic Identity Cards (eIDs)
>A national electronic identity (eID) card can serve the same purposes as other national ID cards. Human-readable data printed on its surface.
>Can provide stronger proof of identity and be used in a wider variety of applications.

#### Password Authenticated Connection Establishment (PACE)
Ensures that contacless RF chip in the eID card cannot be read without explicit access control. For online applications,  access is established by the user entering the six-digit PIN. For offline applications, either the MRZ printed on the back of the card or the six-digit card access number (CAN) printed on the front is used.

### Hardware Authentication Tokens: One-time password (OTP) device
- Has a secret key to generate an OTP
- User enters the OTP and the system validates the value entered
- Uses a block cipher/hash function to combine secret key and time or nonce value to create OTP
- Has a tamper-resistant module for secure storage of the secret key

### Time-based one time password (TOTP)
- Uses HMAC with hash function 
- Used in many hardare tokens and by many mobile authenticator apps
- Password is computed from the current Unix format time value
- Systems using time based OTP need to allow for clock drift between token and verifying system
- Systems using nonce need to allow for failed authentication attempts

>[!note] Pro and Cons
>*Any other person can see the code* -> solution: use of communications link
>Single-factor vs multifactor:
>- Single: provides authentication with just one factor
>- Multi: provides authentication service after a local authentication step

### Authentication Using a Mobile Phone: SMS
- *via message*:

