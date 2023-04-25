# Build a modal window component

## Input properties

1. Define input properties for the colors you want to use: `primaryColor`, `secondaryColor`, `accentColor`
2. Assign your color palette values to them as default values.
![custom properties](/assets/images/cmp_props.png)
3. Create also input properties for radius of buttons, standard width or height of controls you use, and more. The goal is to avoid hard coded values as you don't want to go over the entire component over and over just because someone requests 'just a tiny change' 🙃

## Behavior properties - make your component interact with the app

For this, we can fire custom events with behavior properties - for example we can close a popup-component by

1. Add a behavior property `onClose` (boolean) to our component
2. Add an `X` icon to the component
3. Assign the property to the **OnSelect** of the `X` icon
4. In your component instance, set the **OnSelect** property of your component to `Set(isCmpVisible, false)`
5. In your component instance, set the **Visible** property of your component to `iscmpVisible`

As a result, the component will automagically 🦄 disappear, once a user selects that `X` icon.

💡 Note: If you like behavior properties, you need to first turn on the respecting setting:

![settings](/assets/images/settings.png)

## Content - display useful information with more input properties

As we will also want to give makers good options to customize the content being displayed in the component:

Define input properties for every text, number, table, or image being displayed, such as

1. mainButtonContent
2. labelHeaderContent
3. labelBodyContent

so that makers can easily adjust these values.

## Return values from component to app - Output properties

If users interact with our components and we want to know *what* they did, we will need to return values from our component to the app. We do this with output properties.

For example, if our component contains a TextInput control and we want to know the **Text** property of that in our app, we will need to create an output property, hook that to `TextInput.Text` and then use the Output property in the app to return that value.

## Build the component

Now that you defined all the properties to take care of

1. look and feel of your component
2. content to be displayed
3. inner and outer logic in app context

its time to build the component.

1. Define the components size, preferably relative to the App's **Width** and **Height**
2. Add the controls you need to your component, define **X**, **Y**, **Width** and **Height** relative to the component, don't use hard coded values
Hint: for this modal window, we need a semitransparent rectangle, a non-transparent rectangle, a button, a textinput, some labels and an icon
3. Assign the custom input properties for look and feel: colors and shapes
4. Assign the custom input properties for displaying content: texts, tables, images
5. Assign the behavior properties to the controls that shall call that property like a function
6. Assign the output properties to the controls that shall return a value to the app

## Use the component

Once you finished the component, add it to your app and try it out.

1. Make sure that you assign a custom event to each behavior property
2. Understand the output properties you already defined
