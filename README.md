# Post-to-Slack

[![Automatic Tests](https://github.com/pcolby/post-to-slack/actions/workflows/test.yaml/badge.svg?branch=main)](
  https://github.com/pcolby/post-to-slack/actions/workflows/test.yaml)

Simple GitHub Action for posting messages to Slack.

## Usage

### Post a Basic Message

```yaml
- uses: pcolby/post-to-slack@v1
  with:
    url: ${{ secrets.SLACK_WEBHOOK_URL }}
    text: Hello world!
```

### Post a Customised Message

```yaml
- uses: pcolby/post-to-slack@v1
  with:
    url: ${{ secrets.SLACK_WEBHOOK_URL }}
    text: >-
      Complex message with "quotes", 'quotes',
      and {fancy} [symbols] ;)
    channel: '#general'
    username: '@TestyMcTestface'
    iconEmoji: ':ghost:'
    iconUrl: https://example.com/example.png
```

### Post a Message with Attachments

```yaml
- uses: pcolby/post-to-slack@v1
  with:
    url: ${{ secrets.SLACK_WEBHOOK_URL }}
    text: >-
      Complex message with "quotes", 'quotes',
      and {fancy} [symbols] ;)
    channel: '#general'
    username: '@TestyMcTestface'
    iconEmoji: ':ghost:'
    iconUrl: https://example.com/example.png
    attachments: |
      [
        {
          "fallback":"New open task [Urgent]: <http://url_to_task|Test out Slack message attachments>",
          "pretext":"New open task [Urgent]: <http://url_to_task|Test out Slack message attachments>",
          "color":"#D00000",
          "fields":[
            {
              "title":"Notes",
              "value":"This is much easier than I thought it would be.",
              "short":false
            }
          ]
        }
      ]
```

## Inputs

### `url`

Required *Webhook URL* of a Slack *Incoming WebHook*. To get one:
1. go to [custom integrations] (Slack will require you to login, if not already)
2. click "Incoming WebHooks"
3. click "Add to Slack"
4. choose a channel, and click "Add Incoming WebHooks integration"
5. look for the resulting "Webhook URL", it should look like:

```
https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX
```

Note, the Webhook URL is specific to the Slack workspace it was created for, and must be protected.
As [Slack says]():

> Keep it secret, keep it safe. Your webhook URL contains a secret. Don't share it online, including via public version control repositories. Slack actively searches out and revokes leaked secrets.

For this reason, the URL should be added to the repository's [encrypted secrets], and used like:

```yaml
url: ${{ secrets.MY_SECRET_URL }}
```

And **not**:

```yaml
# Don't do this!!
url: https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX
```

### `text`

Required text for the message to post to a Slack channel. Slack allows the text to include
`\n` for line breaks, and `<a>` tags for links. For example:

* `This is a line of text in a channel.\nAnd this is another line of text.`
* `A very important thing has occurred! <https://alert-system.com/alerts/1234|Click here> for details!`

### `channel`

Optional channel to post the message to. If not set, Slack will use the default channel configured
in the webhook's integration settings.  It should be either a `#channel-name`, or an `@username`.

### `iconEmoji`

Optional Slack emoji to override the default icon configured for the webhook, for example `:ghost:`.

### `iconUrl`

Optional image URL to override the default icon configured for the webhook.

### `username`

Optional name to override the default username configured for the webhook.

### `attachments`

Optional attachments to include with the posted message. Note, since GitHub Action inputs
cannot support complex types, this must be a valid JSON array, serialised as a YAML string.
YAML's block scalar (aka multiline string) support makes this pretty easy, for example:

```yaml
    attachments: |
      [
        {
          "fallback":"New open task [Urgent]: <http://url_to_task|Test out Slack message attachments>",
          "pretext":"New open task [Urgent]: <http://url_to_task|Test out Slack message attachments>",
          "color":"#D00000",
          "fields":[
            {
              "title":"Notes",
              "value":"This is much easier than I thought it would be.",
              "short":false
            }
          ]
        }
      ]
```

Note, it is the caller's responsibility to ensure that `attachments` is valid JSON (serialised
to a YAML string), and meets the requirements of Slack's API. Slack's documentation is sparse in
this area, but some examples can be found by looking at the "Setup Instructions" section when
editing any existing webhook configuration.

### `dryRun`

Really only intended for automated testing, if `dryRun` is set to `true`, then the actual
`POST` to `slackUrl` will be skipped. Callers can still use the [`request`](#request) output
to check what JSON payload *would have* been sent to Slack.

## Outputs

The following Action outputs are available for general diagnostics only.

### `request`

The JSON request payload that was (or would have been, if [`dryRun`](#dryRun) is `true`) submitted
to Slack. Note, this content is actually proceeded with `payload=` in the final `POST` operation.

### `response`

The verbatim response text from Slack.  Typically just `ok`, but can be things like `invalid_payload`,
or `missing_text_or_fallback_or_attachments`.

[custom integrations]: https://www.slack.com/apps/manage/custom-integrations "Custom Integrations"
[encrypted secrets]: https://docs.github.com/en/actions/security-guides/encrypted-secrets "Encrypted secrets"