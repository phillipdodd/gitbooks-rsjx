# Cold vs Hot Observables

| Cold | Hot |
| :--- | :--- |
| Value producer created **inside** the observable | Value producer exists **outside** the observable |
| **One** observer per execution | **Shared producer** allows for **multiple** observers |
| Unicast | Multicast |
| Examples: [interval\(\)](https://rxjs-dev.firebaseapp.com/api/index/function/interval), [ajax\(\)](https://rxjs-dev.firebaseapp.com/api/ajax/ajax) | Examples: Observables wrapping DOM events, Websockets |

{% hint style="info" %}
Using **Subjects**, cold observables can be treated as though they were hot.
{% endhint %}

