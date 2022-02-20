# Acryl study - front-end

> 21-12-23

- [react hooks메커니즘 살펴보기(with. closure)](https://medium.com/@myeongjun222/react-usestate-useeffect-mechanism-with-closure-1fa3da618306)
- [실습환경 - git 저장소](https://github.com/KMJ192/custom-react)

> 22-01-04

- [virtual DOM 정리](https://medium.com/@myeongjun222/%EA%B0%80%EC%83%81-%EB%8F%94-virtual-dom-2b8ca02e0ab6)
- [React diffing algorithm - heuristic](https://kmj24.tistory.com/221)
- [React diffing algorithm - fiber](https://kmj24.tistory.com/222)

- custom virtual dom

```typescript
export interface customElement {
  tagName: string;
  value: any;
  props?: {
    [key: string]: string;
  };
  event?: {
    type: string;
    eventFunc: () => void;
  };
  childNode?: customElement[];
  key?: any;
}
```

- recursion function

```typescript
const creatRealDom = (root: Element, dom?: customElement[] | null) => {
  if (dom === undefined || dom === null) return;

  for (let i = 0; i < dom.length; i++) {
    const { tagName, value, event, props, childNode } = dom[i];

    const element: HTMLElement = document.createElement(tagName);
    if (value !== undefined && value !== null) element.innerText = value;

    if (props) {
      for (const [key, value] of Object.entries(props)) {
        (element as any)[key] = value;
      }
    }

    if (event) {
      const { type, eventFunc: eventRun } = event;
      element.addEventListener(type, eventRun);
    }

    root.appendChild(element);
    if (childNode !== undefined) {
      creatRealDom(element, childNode);
    }
  }
};
```

> 22-02-17

- [Redux 메커니즘에 대한 이해](https://medium.com/@myeongjun222/redux-%EA%B5%AC%ED%98%84-43dcbdee1671)
- [실습환경 - git 저장소(redux 포함, custom라이브러리 react-redux 연결)](https://github.com/KMJ192/custom-react)

### todo list

- react hooks 메커니즘 학습
- virtual dom과 real dom, Diffing algorithm 학습
- redux 내부구조 학습
