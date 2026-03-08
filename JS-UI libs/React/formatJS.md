
__terms__


defaultMessage - declare message here

__message formatting__

text - hello
interpolation - hello {name}  (use key argument for placing value)

__1. FORMAT MESSAGE TAG__

```jsx
import * as React from 'react'
import {IntlProvider, FormattedMessage, FormattedNumber} from 'react-intl'

// Translated messages in French with matching IDs to what you declared
const messagesInFrench = {
  myMessage: "Aujourd'hui, c'est le {ts, date, ::yyyyMMdd}",
}


export default function App() {
  return (
    <IntlProvider messages={messagesInFrench} locale="fr" defaultLocale="en">
      <p>
        <FormattedMessage
          id="myMessage"
          defaultMessage="Today is {ts, date, ::yyyyMMdd}"
          values={{ts: Date.now()}}
        />
        <br />
        <FormattedNumber value={19} style="currency" currency="EUR" />
      </p>
    </IntlProvider>
  )
}
```

__2a. formatMessage - imperative API__

```jsx
// Method must be exactly `intl.formatMessage`
intl.formatMessage(
  {
    description: 'A message', // Description should be a string literal
    defaultMessage: 'My name is {name}', // Message should be a string literal
  },
  {
    name: userName,
  } // Values should be an object literal, but not necessarily every value inside
)
```

__2b. formatMessage - react API__

```jsx
import {FormattedMessage} from 'react-intl'
;<FormattedMessage
  description="A message" // Description should be a string literal
  defaultMessage="My name is {name}" // Message should be a string literal
  values={
    {
      name: userName,
    } // Values should be an object literal, but not necessarily every value inside
  }
/>
```

intl.formatMessage is used to format a message string with the values provided by the user's locale.

- argus: message descriptor (id prop + defaultMessage prop)
- formats message with user's localed

intl.defineMessage
- define a message descriptor object (takes it as an arg)

- { id: used.to.id.msg, defaultMessage: 'if translation not available'}
- - does not format it


__define Message with string literal__

export const confirmationDialogHeading = defineMessages({
  submitionFailed: {
    id: 'confirmation.error.dialog.header',
    defaultMessage: 'Submission failed',
  },
  greating: {
    id: 'confirmation.dialog.header',
    defaultMessage: 'Great to hear from you!',
  },
});


__pull in definition and format it__

  const confirmationDialogHeadingText: string = feedbackError
    ? intl.formatMessage(confirmationDialogHeading.submitionFailed)
    : intl.formatMessage(confirmationDialogHeading.greating);

__pass around formatted message__

        <ConfirmationDialog
        {...confirmationModalProps}
        error={feedbackError}
        dialogHeader={confirmationDialogHeadingText}
        dialogMessage={
          feedbackError
            ? (confirmationDialogErrorMessagesText as string)
            : intl.formatMessage(confirmationDialogMessages.thanksMessage)
        }
      />

__use it__
      <H3 color={colors.textInvert}>{dialogHeader}</H3>