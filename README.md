# Celli Calendar site

A small, dependency-free public website for Kai's private **Celli Calendar** Google OAuth app. It contains a homepage and a privacy policy for Google's external-production branding requirements.

There are no analytics, forms, cookies, external fonts, external scripts, or third-party dependencies.

## Deploy with GitHub and Netlify

1. Create a new **private or public** GitHub repository (for example, `celli-calendar-site`). Do not add a README or `.gitignore` if you are uploading this directory as-is.
2. From this directory, commit and push the files:

   ```sh
   git init
   git add index.html privacy/index.html styles.css README.md .gitignore
   git commit -m "Create Celli Calendar public site"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/celli-calendar-site.git
   git push -u origin main
   ```

3. In Netlify, choose **Add new site → Import an existing project**, select GitHub, and choose the repository.
4. Use these build settings:
   - **Build command:** leave blank
   - **Publish directory:** `.` (the repository root)
   - **Base directory:** leave blank
5. Deploy. Netlify will provide an HTTPS URL such as `https://celli-calendar.netlify.app/`.
6. If you want updates to publish automatically, keep the repository connected to Netlify. A push to `main` will trigger a new deploy.

### Choose a Netlify subdomain

Before entering URLs in Google Cloud, choose a stable site name. In Netlify, open the site and go to **Site configuration → General → Site details → Change site name** (the exact label may vary slightly in the current Netlify UI). Pick a name such as `celli-calendar`; the default subdomain will then be:

```text
https://celli-calendar.netlify.app/
```

The name must be available. Treat this URL as public, keep the site name stable after OAuth review, and use the HTTPS URL rather than a `netlify.app` HTTP URL. A custom domain can be connected later, but update Google's URLs if the public origin changes.

## Google Cloud branding URLs

In the Google Cloud project used by Celli Calendar, enter these exact URL forms under the OAuth consent screen / Branding configuration. Replace `YOUR-SITE-NAME` with the chosen Netlify site name:

- **Application home page:** `https://YOUR-SITE-NAME.netlify.app/`
- **Application privacy policy link:** `https://YOUR-SITE-NAME.netlify.app/privacy/`

For example, if the chosen name is `celli-calendar`, enter:

- `https://celli-calendar.netlify.app/`
- `https://celli-calendar.netlify.app/privacy/`

The homepage and privacy policy must be reachable publicly without a login. If you later attach a custom domain, use the corresponding exact URLs instead (for example, `https://calendar.example.com/` and `https://calendar.example.com/privacy/`) and make sure the domain is visible in the Google Cloud project configuration.

The privacy policy currently lists `kairusxdelgado@gmail.com` as its monitored public contact address. Update both the visible address and its `mailto:` link in `privacy/index.html` if that contact changes.

## Google Search Console caveat

Search Console verification is separate from Google OAuth branding and is not needed just to host these pages. If Search Console asks for verification, use a URL-prefix property and verify through an available method (such as an HTML file deployed in this repository or an HTML meta tag), or verify a domain through DNS if you control the domain. Netlify's deploy URL and any custom domain are different properties. Verification does not require adding analytics or tracking to this site.

## Local check

Because this is a static site, it can be served locally with Python:

```sh
python3 -m http.server 8000
```

Then open `http://localhost:8000/` and `http://localhost:8000/privacy/`.
