# Slack Deploy Hooks
> The Khan deployment service for Slack

Slack Deploy Hooks replace the old Sun Wukong Hubot plugin with a much simpler
webhook-based solution that otherwise works identically.

## Making a deploy

### Prerequisites
You will need to install Node and npm through the usual channels (0.12.7
or higher, please), and will also need a working `gcloud` tool for deploying.

Node can be install via the usual `brew install node`.

Set up the gcloud tool as [per instructions][gcloud-install]. (Note
that on Mac you can use `brew cask install google-cloud-sdk` instead of their
installer, if you prefer.)

[gcloud-install]: https://cloud.google.com/container-engine/docs/before-you-begin#install_the_gcloud_command_line_interface

### Development

First, you can optionally provision secrets locally. Instructions will be
given on your first deploy.

The Slack deploy hooks are a vanilla Node application, so a simple

    $ npm install
    $ export SUN_DEBUG=1
    $ npm run monitor

Will give you a fully set-up local copy of khan-sun. You can then easily test
it simply by using a tool like httpie and submitting Slack outgoing webhooks
and observing the result. For example, to test the sun: ping command:

    http -f POST :8080/ \
         team_id=T0001 team_domain=example \
         channel_id=C2147483705 channel_name='bot-testing' \
         user_name=bmp text='sun: ping' trigger_word=sun:

Should give you the response like `{}`, indicating success, from the HTTP
command, and print out the response text in the terminal running Sun. (If you
do not see any output, you probably forgot to set the `SUN_DEBUG` flag specified
above.)

### Build and Deploy

All you have to do is run `npm run deploy` and follow directions. That's it.
