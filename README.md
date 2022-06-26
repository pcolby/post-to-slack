# Post-to-Slack

[![Automatic Tests](https://github.com/pcolby/post-to-slack/actions/workflows/test.yaml/badge.svg?branch=main)](
  https://github.com/pcolby/post-to-slack/actions/workflows/test.yaml)

Simple GitHub Action for posting messages to Slack.

## Usage

### Post a Basic Message

```yaml
- uses: pcolby/post-to-slack@v1
  with:
    url: https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX
    text: Hello world!
```

### Post a Customised Message

```yaml
- uses: pcolby/post-to-slack@v1
  with:
    url: https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX
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
    url: https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX
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

### url

### text

### channel

### iconEmoji

### iconUrl

### username

### attachments

### dryRun

## Outputs

### request

### response
