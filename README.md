# Setup

1. Clone the repo:
   git clone https://github.com/SPIRAME/Emudhroll && cd Emudhroll
2. Install requirements:
   pip install -r requirements.txt
3. Run the proxy:
   python main.py
4. Permanent unenrollment mode:
   python main.py --permanent
5. Re-enroll:
   python main.py --enroll

The proxy listens on port 8080.

## Chromebook setup (normal unenroll)

1. Powerwash the Chromebook.
2. On the OOBE screen, connect to Wi-Fi and open its proxy settings. (it is necessary to do it on the welcome as revocation will occur otherwise if not done fast enough)
3. Set to Manual proxy configuration.
4. Enable Use the same proxy for all protocols.
5. Enter your computer's IP and port 8080.
6. Continue through OOBE and it should unenrolol
7. Note: If it says can't reach google and you are sure the chromeboook is on versions 152 and below then simply powerwash and try again (it means revocation occured and the client no longer trusts the emudhra cert)

## Permanent unenrollment (--permanent)

1. Start the proxy: python main.py --permanent
2. Go through OOBE on the Chromebook.
3. Powerwash the device after the proxy says it unenrolled
4. Once powerwashed, It will successfully unenrollol

## Re-enroll (--enroll)

1. Run: python main.py --enroll
2. Enter the stable device secret (hex) when prompted (this is obtained via entering devmode and running vpd -l as root in vt2)
3. On powerwash, it will successfully reenroll

## Credits

1. Lxrd for for getting the unenrollment to work using the Emudhra CA Compromise
2. Katie for improving the scripts
3. Emudhra thank you for your incompetency

[Join the Discord](https://discord.gg/d3B2FtxrpF)
