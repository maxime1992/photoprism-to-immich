# Purpose

Easily migrate your entire Photoprism library to Immich.

# Features

- Import all your Photoprism assets to Immich. It works for pictures, videos, animations (GIF) or even live photos
- Preserve your albums (title at least)
- Preserve your favourite assets as such
- Preserve the GPS coordinates that have been added manually to Photoprism and that are not part of EXIF metadata

# Disclaimer

The code is ~300 lines of JS and 0 external dependencies. It's fairly simple. I strongly advise you to take a look at the code before running it and I shall not be responsible if anything goes wrong on your side.

Tested with Photoprism `Build 240711-2197af848` and Immich `v1.115.0`.

This has been tested on a brand new Immich server as I had everything on Photoprism. I would not recommend to run that on an Immich server that already has "production" data in case it messes anything up.

It worked perfectly in my case for +15k assets, hopefully it goes as smoothly for you.

# Get an access token for Photoprism

On your Photoprism instance go to `/library/settings/account` and click on "App and devices".

Copy the token to the `.env` in the `photoprism.accessToken` entry.

Also update the URL if needed to point to your Photoprism instance.

# Get an access token for Immich

On your Immich instance go to `/user-settings?isOpen=api-keys` and click on "New API Key".

Copy the token to the `.env` in the `immich.apiKey` entry.

Also update the URL if needed to point to your Immich instance.

# Start the script

Both Photoprism and Immich must be running before launching the following command as the migration is done using their respective APIs.

```bash
docker run --rm --network=host -v .:/app -v /home/your-user/path-to-photoprism/photoprism/originals:/originals:ro -w /app node:22.9.0 node index.js
```

You shall see logs along the way to know how much is left but it can take several hours depending on how powerful is your server and how many assets you've got. On top of that, once all the uploads are done, Immich will most likely run for a while to process it all. You'll be able to see all the pending tasks here `/admin/jobs-status`.

# Cleanup

Remove the API keys created in both systems once the migration is done.
