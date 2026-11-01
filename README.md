# Setup

1. Install requirements:
   pip install -r requirements.txt
2. Run the proxy:
   python main.py
3. Permanent unenrollment mode:
   python main.py --permanent
4. Re-enroll:
   python main.py --enroll

The proxy listens on port 8080.

## Chromebook setup (normal unenroll)

1. Powerwash the Chromebook.
2. On the OOBE screen, connect to Wi-Fi and open its proxy settings.
3. Set to Manual proxy configuration.
4. Enable Use the same proxy for all protocols.
5. Enter your computer's IP and port 8080.
6. Continue through OOBE and it should unenrolol

## Permanent unenrollment (--permanent)

1. Start the proxy: python main.py --permanent
2. Go through OOBE on the Chromebook.
3. When prompted, powerwash the device then press y.
4. On powerwash, It will successfully unenrollol

## Re-enroll (--enroll)

1. Run: python main.py --enroll
2. Enter the stable device secret (hex) when prompted.
3. On powerwash, it will successfully reenroll

## Credits

1. Lxrd for for getting the unenrollment to work using the Emudhra CA Compromise
2. Katie for improving the scripts
