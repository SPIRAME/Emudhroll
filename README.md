# Emudhroll

4 🥹

## Table of Contents

- [Step 1: Proxy Setup](#step-1-proxy-setup)
- [Step 2: Temporary Unenrollment](#step-2-temporary-unenrollment)
- [Step 3: Permanent Unenrollment (Optional, requires WP disabled)](#step-3-permanent-unenrollment-optional-requires-wp-to-be-disabled)
- [Credits](#credits)

## Step 1. Proxy Setup

1. Clone the repo: `git clone https://github.com/SPIRAME/Emudhroll && cd Emudhroll`
2. Install requirements: `pip install -r requirements.txt`
3. Run the proxy: `python main.py` (you may need to use `python3 main.py` depending on your system)

The proxy listens on port `:8080`.

## Step 2. Temporary Unenrollment

This works on version 152 and below (if it doesn't work on 152, try a lower version)

1. Powerwash the Chromebook.
2. On the "Welcome" OOBE screen, connect to Wi-Fi from the Quick Settings tray (in the bottom right), click the settings/gear icon, open up Proxy settings in the popup dialog that appears. (it's required to enable the proxy on the "Welcome" screen, as revocation will occur otherwise if not done fast enough)
4. Set to Manual proxy configuration
5. Enable Use the same proxy for all protocols
6. Enter your computer's IP and port 8080
7. Continue through OOBE and it should unenrolol

For every failed attempt, you must restart from step 1, as there is a 99% chance that the certificate got revoked.

### Notes
- If you see a "Can't reach Google" error screen and the Chromebook is on version 152 or below, powerwash and try again.
  - (this indicates revocation occurred and the client no longer trusts the eMudhra certificate)
- Another edge case is the Chromebook not actually connecting to the proxy due to firewall issues on the host, powerwashing will not help in this case as the issue would need to be resolved on the host side.
  - (indicative of no requests being logged in verbose mode)

## Step 3. Permanent Unenrollment (Optional, requires WP to be disabled)

This step is *completely optional*, but every time you powerwash your device or transition it between Normal and Developer mode, you will need to do steps 1 and 2 on every OOBE. This might not be a deal-breaker to some people, but you've been warned.

This step also assumes that you are tech-savvy enough to not be allergic to a terminal.
If you're a skid who's deathly afraid of touching a terminal and/or a chance of needing to open up your Chromebook (depending on your model), **turn back now and stick with the temporary unenrollment**.

Any mistakes can range from minor inconveniences to downright ***bricking your Chromebook***.
If you end up bricking your Chromebook because of *your own mistake*, we are **not responsible nor libable** for that, **you** are.
You have been warned.

1. Transition to Developer Mode (`Esc + Refresh + Power`, `Ctrl + D`, `Enter`, wait ~10 mins)
1.5. \[Optional but recommended] Set up a root user with your own password (use the password `root` if you can't come up with one)
2. Repeat steps 2-6 of the [temporary unenrollment](#step-2-temporary-unenrollment) section
3. Enter the VT2 shell. (`Ctrl + Alt + F2` / `Ctrl + Alt + 🡪`)
4. Log in as `chronos`. (When prompted for a password, just press `Enter`, the `chronos` user has no password by default!)
   - If you did step 1.5, and you are not able to log in as `chronos` without a password, you can also log in as `root` with the password you set.
5. Check your current VPD values with `vpd -l`. To continue, you must see `stable_device_secret_DO_NOT_SHARE`.
6. Change your stable device secret with the following command:
   ```sh
   sudo vpd -s "stable_device_secret_DO_NOT_SHARE"=$(openssl rand -hex 32)
   ```
   You may also use your own value instead of `$(openssl rand -hex 32)`, but it is generally recommended to keep the format the same.

### Notes

If you experience any issues with any of these steps, it's possible that you're about to go on a trip on the internet (and if you're into it, talk with an LLM about it), since these some of steps could vary per person. This is most likely to be true with step 6.

## Credits

1. Lxrd for for getting the unenrollment to work using the eMudhra CA compromise
2. Katie for improving the scripts
3. eMudhra thank you for your incompetency

[Join the Discord](https://discord.gg/d3B2FtxrpF)
