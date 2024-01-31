# Tailwind Dynamic Class Names

For my fellow Tailwind and React enthusiasts, have you ever tried to dynamically apply the class names based on the props that you receive in your component? 🤔

Let's say we have a component called `CustomButton`.

```jsx
const CustomButton = ({color}) => {
    return (
        <button className={`bg-${color}-700`}>
            Hello World
        </button>
    );
}
```

Here, `CustomButton` is a reusable component that receives **color** as a prop. The idea is to dynamically style the button's background color based on the prop it receives.

Now, let's use two instances of `CustomButton` within a `ButtonContainer` component.

```jsx
const ButtonContainer = () => {
    return (
        <>
            <CustomButton color="red"/>
            <CustomButton color="violet"/>
        </>
    )
}
```

The first one has `color="red"` as a prop, and the second one has `color="violet"` as a prop.

The idea is that the first button will have the `bg-red-700` class name, and the second one will have the `bg-violet-700` class name. So, the expected result is that the first button will have a red background color, and the second one will have a violet background color.

The code seems good, so let's check the result ... 🥁🥁🥁

<p style="text-align: center; margin-top: 40px;">
  <img src="failed-demo.png" alt="failed-demo" style="border-radius: 16px"/>
</p>

It didn't work. 🤯🤯🤯

We do know that `bg-red-700` and `bg-violet-700` are valid Tailwind class names.  But those two buttons didn't have the background color that we expected.

Hmm, why does this happen? 🤔

This is actually one of the common _gotcha_ when using Tailwind. The reason is that _Tailwind can only detect classes that exist as **complete unbroken strings** in our source code._

The keyword is: **complete unbroken strings**.

Let's look once again at how we dynamically apply the class name to our button.

```jsx
<button className={`bg-${color}-700`}>
    Hello World
</button>
```

As we see in the code above, we dynamically apply the class name using a template literal. Even though the result of the template literal is `bg-red-700` and `bg-violet-700`,  those class names don't exist as **complete unbroken strings** , and Tailwind doesn't allow us to do that. 😢

To address this, let's consider this straightforward solution:

```jsx
const ButtonContainer = () => {
    return (
        <>
            <CustomButton color="bg-red-700"/>
            <CustomButton color="bg-violet-700"/>
        </>
    )
}

const CustomButton = ({color}) => {
    return (
        <button className={`${color}`}>
            Hello World
        </button>
    );
}
```

Here, we pass the complete class name as a prop to the `CustomButton` component, ensuring our classes exist as **complete unbroken strings**.

Let's check the result … 🥁🥁🥁

<p style="text-align: center; margin-top: 40px;">
  <img src="success-demo.png" alt="success-demo" style="border-radius: 16px" />
</p>

Done! It works as expected now! 🎉🎉🎉

Just remember the keyword: **complete unbroken strings** 😉

Congratulations on learning this new tip today! 😄

---

reference:
- https://tailwindcss.com/docs/content-configuration#class-detection-in-depth
- https://tailwindcss.com/docs/content-configuration#dynamic-class-names
