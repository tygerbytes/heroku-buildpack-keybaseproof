# Heroku Buildpack: keybaseproof

This buildpack enables deploying a keybase proof to an arbitrary directory from either a URL or a Heroku config variable.

## Description
You want to deploy your Keybase proof to your Heroku-powered website, but you don't want to store the proof along with your Git repo. Just add this buildpack to your project and a few config vars and you're set.

## Usage

### Add your config variables:

variable | description
--- | --- 
`KEYBASEPROOF_DEPLOY_DIR` | The directory to deploy `keybase.txt`. Relative to your app. (*Example: `public`*) | 
`KEYBASEPROOF_TEXT` | contains the full text of your keybase proof |
`KEYBASEPROOF_URL` | URL that points to your publicly hosted proof text |

You must configure either `KEYBASEPROOF_TEXT` *or* `KEYBASEPROOF_URL`. If you add both, `KEYBASEPROOF_TEXT` will be used.

If you choose to use `KEYBASEPROOF_URL`, ensure the URL is highly available or you risk breaking your build. For that reason, favor using `KEYBASEPROOF_TEXT` where possible.

### Add the buildpack to your Heroku app:

     heroku buildpacks:add https://github.com/tygerbytes/heroku-buildpack-keybaseproof.git

### Example

Let's put it all together in a scripted example. 

Scenario: You want to deploy keybase.txt to your app's `public` directory from the `KEYBASEPROOF_TEXT` config var. `./keybase.txt` contains your proof text locally.

     heroku config:set KEYBASEPROOF_DEPLOY_DIR=public     
     heroku config:set KEYBASEPROOF_TEXT="$(< ./keybase.txt)"
     heroku buildpacks:add https://github.com/tygerbytes/heroku-buildpack-keybaseproof.git

That's it. Once you've set those config vars, your keybase proof will be deployed with every build.

## License
MIT. See [LICENSE.md](LICENSE.md).
