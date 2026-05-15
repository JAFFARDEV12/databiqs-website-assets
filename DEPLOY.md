# Deploy databiqs-website-assets

## 1. Push to GitHub

```powershell
cd E:\Work\Databiqs-Projects\company-website\databiqs-website-assets
git add .
git commit -m "chore: sync static assets for CDN"
git branch -M main
git remote add origin https://github.com/JAFFARDEV12/databiqs-website-assets.git
git push -u origin main
```

## 2. Vercel

1. [vercel.com/new](https://vercel.com/new) → Import `JAFFARDEV12/databiqs-website-assets`
2. Framework: **Other** | Build command: *(empty)* | Output: **`.`**
3. Deploy → note URL, e.g. `https://databiqs-website-assets.vercel.app`

## 3. Main website env

```env
REACT_APP_ASSETS_CDN_URL=https://databiqs-website-assets.vercel.app
```

Set on Vercel (main app) and in `databiqs-website/.env.local`.

## 4. Verify & remove local copies

```powershell
cd ..\databiqs-website
$env:REACT_APP_ASSETS_CDN_URL="https://databiqs-website-assets.vercel.app"
npm run assets:verify
npm run build
npm run assets:remove-dry
npm run assets:remove
```

## Re-sync after asset changes

```powershell
cd ..\databiqs-website
npm run assets:sync
cd ..\databiqs-website-assets
git add . && git commit -m "chore: sync assets" && git push
```
