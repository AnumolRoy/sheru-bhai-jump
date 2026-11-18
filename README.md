# Sheru Jump

A tap-to-fly mobile game. Sheru Bhai flies through the pipes. Pass obstacles to climb the score ladder:
100 → 1,000 → 1 Lakh → 10 Lakh → 1 Billion → 1 Trillion (the ultimate goal). Every stage you clear pays gold coins, and coins in the gaps add more.

## Files

- `index.html`: the whole game (works on phones, tablets and desktops)
- `manifest.webmanifest` and `icon.svg`: lets the game install to a phone's home screen like an app

## Play on your phone (quickest way)

1. Put this folder online with a free static host, for example:
   - **Netlify Drop**: go to app.netlify.com/drop and drag the `sheru-jump` folder onto the page. You get an https link.
   - **GitHub Pages**: push the folder to a GitHub repo, then turn on Pages in the repo settings.
2. Open the link on your phone.
3. Install it to the home screen:
   - Android (Chrome): menu (⋮) → **Add to Home screen** / **Install app**
   - iPhone (Safari): Share → **Add to Home Screen**

The game needs https (or localhost) for the install option. Sound starts after your first tap, which is normal for phones.

## Build a real Android APK (Play Store / sharing as an app)

This wraps the same game in a native Android app using Capacitor. You need Node.js and Android Studio installed.

```bash
cd D:\claude-code\sheru-jump
npm init -y
npm install @capacitor/core @capacitor/cli @capacitor/android
npx cap init "Sheru Jump" com.sherubhai.jump --web-dir=.
npx cap add android
npx cap copy
npx cap open android
```

In Android Studio: **Build → Build Bundle(s) / APK(s) → Build APK(s)**. For the Play Store, use **Generate Signed Bundle** and upload the `.aab` file to Google Play Console.

Note: `--web-dir=.` points Capacitor at this folder. If you add extra folders later, move `index.html` into a `www/` folder and use `--web-dir=www` instead.

## Difficulty and tuning

Edit the values at the top of the script in `index.html`:

- `STAGES`: the score targets and labels
- `spawnPipe()`: the first 5 obstacles are wide (220px gap) and slow. After that the gap shrinks toward 118px.
- `currentSpeed()`: slow (1.5) for the first 5 obstacles, then speeds up gradually to a cap of 4.0
- `pointsForObstacle()`: each obstacle is worth 25% of your current score (minimum 10), so reaching a trillion takes around 100 obstacles
- `COIN_VALUE` and the stage bonus (`100 × stage number`)
