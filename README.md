# Fancy Footage Club

Free, cinema-quality stock footage loops, released monthly through 2015 by
Andrew Nater and Kevin HG. The club has closed; the library stays up so the
footage can still be downloaded and used.

A Jekyll 4 site. Locally, with Ruby 3.x: `bundle install`, then
`bundle exec jekyll serve`.

## Hosting (2026)

Since October 2026 Kevin HG hosts the site, with Andrew's okay:

- **Site:** a Vercel project serving https://ffc.kevinhg.com and
  https://ffc.trimm.co, built with Vercel's Jekyll preset (Ruby 3.3).
- **Footage:** a Cloudflare R2 bucket at https://media.ffc.kevinhg.com/,
  set in `_config.yml` as `dlurl` (zips, `loops/`) and `asseturl` (previews,
  posters and thumbnails, `website/`).

Why it moved: the site ran on Andrew's Netlify account, with footage in his
S3 bucket `fancyfootageclips`. A second bucket, `fancyfootage.club`, held the
original favicons and the 404 and thank-you pages' styles, scripts and video;
it has been deleted, so those pages were already broken. The
fancyfootage.club domain expired on 2026-10-18 and was not renewed. The
footage was copied from S3 to R2 key-for-key (272 objects), so only the two
base URLs changed. Everything the deleted bucket served now comes from this
repo or the R2 bucket, and the site's contact address is ffc@trimm.co (an alias on Kevin's mailbox).

Three Vercel notes, all in `vercel.json`:

- The build command is pinned to `bundle exec jekyll build`. Without it
  Vercel runs `package.json`'s `build` script (`grunt && jekyll build`), and
  the 2015 Grunt setup has no `grunt` command, so the build would fail. The
  CSS Grunt builds is already committed (`css/main.min.css`).
- The install command pins Bundler's gem folder to `vendor/bundle`, so the
  build step finds the gems whatever `GEM_HOME` Vercel sets, and it skips
  an `npm install` of that unused Grunt tooling.
- `/library/2015/03/usflag/` is served too, because Netlify lowercased that
  one URL and the real page is `/library/2015/03/USflag/`.
