# PowerApps-Masterclass

## Agenda

### intro & logistics - 20 minutes

- presenters
- structure of the day
- topics, breaks, logistics
- create Power Platform developer account

### Prefacing the day

- Why does performance, accessibilty and good design matter?
- Some bad examples

### Start with data

- Intro to DV - what differentiates it from SP list?
- Why Excel is evil
- Why is Dataverse is so fast, and on prem is slow?

### COFFEE BREAK

### good coding practices

- collections (locally)
- concurrence - 5 minutes
- use galleries when repeat
- use components when not working with galleries

### components

- intro to components
- How to plan components
- Build a modal window component
- Build a swipe right component

### Intro to accessibility and how to make apps accessible by design - 20 minutes

- situational, temporary, permanent
- accessibility checker
- How to measure accessibility
- WCAG standard
- dev tools
- windows built in tools

### Are accessibility requirements a constraint or an opportunity?

- explaination: how does that tie in with good design an accessiblity - 10 minutes
- task: add accessibility features to our cmp - 10 minutes
- accessible label, tab

### Multilanguage apps

- how to make apps multilingual - 20 minutes - live demo
- no hard coded values in the app (front end) but only in the data source (back end)
- task: add a 2nd language to the app - 30 minutes
  - manually
  - cloud flow with translater which adds the words to a DV localization table
  - Use LookUp and a filtered collection

### Responsive Apps that look good on any screen

- intro to responsive screens (containers, v,h, c, breakpoints, label:  App.width) - 15 minutes
- task: create a screen with containers based on a screenshot (try to replicate this!) - test everything on different screen sizes (dev tools) - 15 minutes

### how to use visual hierarchy and layouts to make your applications more accessible and comprehensible - 10 minutes

- reduce content on the screen, legible, supplement text with icons, separate content to give visual cues
- final task: give them an awfully designed screen: how many mistakes do you find? 15 minutes
- can you fix them? - 40 minutes
  - missing AccessibleLabel
  - too much content
  - bad contrast ratio
  - tabs that are not a gallery
  - modal window that is not a component
  - no collections used
  - hard coded values
- present if you feel confident
