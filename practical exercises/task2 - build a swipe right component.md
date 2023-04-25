# Let's build a swipe right component

![swipe right components](/assets/images/swiperight.gif)

## Create the Component with custom properties

1. Create a new component `cmp_SwipeRight` and add the following custom properties

| property          | type              | default               |
|-------------------|-------------------|-----------------------|
| **swipeHeight** | Number            | `55`                    |
| **swipeWidth**  | Number            | `250`                   |
| **primaryColor**      | Color             | `ColorValue("#c0c0c0")` |
| **secondaryColor**    | Color             | `RGBA(116,116,116,1)` |
| **accentColor**    | Color             | `RosyBrown` |
| **textColor**         | Color             | `White`                 |
| **backgroundText1**        | Text              | `"swipe to approve"`                |
| **backgroundText2**        | Text              | `"thank you"`                |
| **chevronColor1**         | Color             | `White`                 |
| **chevronColor2**        | Color             | `LightGray`                 |
 **chevronColor3**        | Color             | `DarkGray`                 |
  **icon**        | Image             | `Icon.Heart`                 |
| **Onchange**          | Behavior(Text)    | (needs number parameter called `valueslider`)|

2. Set the **Width** property of the component to `cmp_SwipeRight.swipeWidth+10` and the **Height** property to `cmp_SwipeRight.swipeHeight+20`

### background button

1. Add a button `btn_background_1`, set its **DisplayMode** property to `View` - We don't want people to interact with this button. The only reason this is not a text label is that we can't do rounded corners with a text label 🙄
2. Set the **Fill** property to `cmp_SwipeRight.primaryColor`, the **BorderColor** property to `Self.Fill` and the **Color** property to `cmp_SwipeRight.textColor`
3. Position the button to **X** = `(Parent.Width-Self.Width)/2` and **Y** = `(Parent.Height-Self.Height)/2`
4. Set the **Width** property to `Parent.Width-10` and the **Height** property to `Parent.Height-10`
5. Set the **Border radius** to `10` (it's the default value)
6. Set the **Align** property to `Align.Center`
7. Set the **Text** property to `If(sli_swipeRight_1.Value<100,cmp_SwipeRight.backgroundText1,cmp_SwipeRight.backGroundText2)` - don't worry, this will give an error as we are referring to a slider control that doesn't exist yet - we will fix this in the next step.

### slider

You guessed it - we need a slider control.

1. Add a horizontal slider control, set its **Min** to `0` and its **Max** to `100`, **Default** is `0` as well
2. Set its **HandleSize** to **200**
3. Set **X** to `btn_background_1.X+5` and **Y** to `0`
4. Set **Width** to `cmp_SwipeRight.swipeWidth-btn_swipe_1.Width-12` and **Height** to `Parent.Height`
5. Set _all_ color values to `Transparent` - this control should be invisible to users - still  resist that urge to set the **Visible** property to `false` - users can't interact with the control anymore if you do that
6. Set the **OnChange** property to `If(Self.Value<100, Set(isActionSuccess, false), Set(isActionSuccess, true)); cmp_SwipeRight.Onchange(Self.Value)` - We determine if a user has (completely) swiped right and output this into a variable.

### swipe button

As we don't want users to see the slider handle (you can't change its shape), we need something else so that they know that they swiped :-)

1. Add a button `btn_swipe_1` and again set its **DisplayMode** property to `View` - this is just to be pretty, not to have users interact with it directly
2. Set **X** to `sli_swipeRight_1.X+ sli_swipeRight_1.Width/100*sli_swipeRight_1.Value+1` and **Y** to `(Parent.Height-Self.Height)/2` - which means that our swipe button moves alongside with the (hidden) handle of the slider
3. Set **Height** to `btn_background_1.Height-20` and **Width** to `Self.Height`
4. Set **Fill** to `cmp_SwipeRight.secondaryColor` and **BorderColor** to `Self.Fill`
5. Set the **Text property** to `""` - we don't need any text in here - the entire magic is done in a gallery

### gallery

Speaking of a gallery - we need this to show those nice chevrons!

1. Create a horizontal gallery `gal_chevrons`
2. Set its **items** property to

```powerappsfl
Table(
    {
        id: 1,
        icon: Icon.ChevronRight,
        color: cmp_SwipeRight.chevronColor1
    },
    {
        id: 2,
        icon: Icon.ChevronRight,
        color: cmp_SwipeRight.chevronColor2
    },
    {
        id: 3,
        icon: Icon.ChevronRight,
        color: cmp_SwipeRight.chevronColor3
    }
)
```

3. Set **X** to `sli_swipeRight_1.X+ sli_swipeRight_1.Width/100*sli_swipeRight_1.Value+1` and **Y**  to `btn_swipe_1.Y` - which means that our gallery will _stick_ to our swipe button when it moves
4. Set its **Width** to `btn_swipe_1.Width` and its **Height** to `btn_swipe_1.Height`
5. Set **TemplatePadding** to `1` and **TemplateSize** to `12`
6. Set **Visible** to `!isActionSuccess` - remember, this is set when we move the slider :-) As a result, the gallery wil disappear once we swiped
7. Add an icon `icon_chevron` to that gallery
8. Set the **Icon** property of the icon to `ThisItem.icon`
9. Set its **Height** to `Parent.Height` and its **Width** to `15`
10. Set the **Color** property to `ThisItem.color`

This empty swipe button should  now indicate, that the swipe was a success:

### icon

1. Add an icon to your component
2. Set **X** to `btn_swipe_1.X+ (btn_swipe_1.Width-Self.Width)/2` and **Y** to `btn_swipe_1.Y+(btn_swipe_1.Height-Self.Height)/2`
3. Set **Width** and **Height** to `16`
4. Set **Color** to `cmp_SwipeRight.accentColor`
5. Set the **icon** property of the icon to `cmp_SwipeRight.icon`
6. Set **Visible** to `isActionSuccess` - as a result once the gallery disappeared, the single icon shows up

WE now want to add some more 3D effect to our component and have a nice shadow on the swipe button.

### HTMLtext

1. Add an HTMLText control `html_shadowSwipe_1` to the component
2. Set **X** to `sli_swipeRight_1.X+ sli_swipeRight_1.Width/100*sli_swipeRight_1.Value-10` and **Y** to `4` - this way it moves along with the swipe button and the gallery
3. Set **Width** to `btn_swipe_1.Width+25` and **Height** to `btn_swipe_1.Height+25`
4. Set its **HTMLText** property to `"<div style='margin:5px;width:"&btn_swipe_1.Width&"px;height:"&btn_swipe_1.Height&"px;background-color:#;box-shadow:3px 6px 6px 1px rgba(0,0,0,0.14); border-radius:"&btn_swipe_1.RadiusBottomLeft&"px'></div>"`

## Bring all controls into the right order

Make sure that all controls sit like this:

![swipeRight component controls](/assets/images/swipe-controls.png)

## Add the component to your app

Now let's add the component to our app and play around with the appearance - as we set a ton of custom properties for colors, sizes, and icon, we can easily adjust the look of this component. You can try out for example to change the colors of the chevrons depending on the Fill color of  your swipe button or different icons  to determine success and of course different texts.

Still one thing is missing - we need to know when our user swiped, right? To do so, set the (custom) **Onchange** property of the component to `UpdateContext({loc_isSuccessValue: valueslider})` - This way we set a local variable that returns a `100` if the slider was swiped completely.
