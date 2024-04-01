---
modified: 2024-03-31T15:48:41+02:00
---
```ts
type User = {
  name: string
  age: number
}

const isUserLegal = (user: User, guardianApproval: boolean) => {
  if(user.age >= 18 || guardianApproval) {
    return true
  }
  return false
}
```

```json
[
{
  "kind": "typeAliasDeclaration",
  
},
{
  "kind": "arrowFunction",
  "parameters": [{
    "type": "reference",
  }],
  "body": {
    "kind": "block",
    "statements": [{
      "kind": "ifStatement",
      "expression": 
    }]
  }
}]
```

```json
{
  "kind": "arrowFunction",
  "parameters": [{
    "name": "user"
    "type": "reference",
    "reference": "User"
  }],
  "return": [{
    "value": true,
    "condition": {
      "kind": "binaryExpression",
      "left": {
	      "kind": "propertyAccessExpression",
	      "property": "age",
	      "expression": "user"
      },
      "operator": ">=",
      "right": {
        "kind": "numericLiteral",
        "text": "18"
      }
    }
  }, {
    "value": false,
  }]
}
```

```json
[{
  "return": true,
  "cases": [{
    "Parameters<typeof isUserLegal>[0]['age']": {
      "type": number,
      "inclusiveRange": [18, Infinity]
    }
  }, {
    "Parameters<typeof isUserLegal>[1]": {
      "type": boolean,
      "value": true
    }
  }]
}, {
  "return": true,
  "cases": [{
    "Parameters<typeof isUserLegal>[0]['age']": {
      "type": number,
      "exclusiveRange": [-Infinity, 18]
    }
  }, {
    "Parameters<typeof isUserLegal>[1]": {
        "type": boolean,
        "value": false
    }
  }]
}]
```

```ts

type User = {
  name: string
  age: number
}

const isUserLegal = (user: User, approved: boolean) => {
  if(user.age >= 18 && guardianApproval) {
    return true
  }
  return false
}
```

```json
[{
  "return": true,
  "cases": [{
    "Parameters<typeof isUserLegal>[0]['age']": {
        "type": "number",
        "ranges": [{
          "inclusive": [18, Infinity]
        }],
        "and": {
	       "Parameters<typeof isUserLegal>[1]": {
	         "type": "boolean",
	         "value": true
	       }
	    }
    }
  }]
}, 
{
  "return": false,
  "cases": [{
    "Parameters<typeof isUserLegal>[0]['age']": {
        "type": "number",
         "ranges": [{
          "exclusive": [-Infinity, 18]
         }]
    },
    "Parameters<typeof isUserLegal>[1]": {
        "type": "boolean",
        "value": false,
    }
}]
```
_or_
```json
[{
    "Parameters<typeof isUserLegal>[0]['age']": {
        "type": "number",
        "cases": [
            {
                "ranges": [{
                    "inclusive": [18, Infinity]
                }],
                "returnCases": [{
                    "Parameters<typeof isUserLegal>[1]": {
                         "type": "boolean",
                         "value": true,
                         "return": true
                    },
                }, {
                    "Parameters<typeof isUserLegal>[1]": {
                         "type": "boolean",
                         "value": false,
                         "return": false
                    },
                }],
            }, {
                "ranges": [{
                    "exclusive": [-Infinity, 18]
                }],
                "returnCases": [{
                    "Parameters<typeof isUserLegal>[1]": {
                         "type": "boolean",
                         "value": true,
                         "return": false
                    },
                }, {
                    "Parameters<typeof isUserLegal>[1]": {
                         "type": "boolean",
                         "value": false,
                         "return": false
                    },
                }],
            }
        ],
    }
}]
```


```ts
describe('when `user.age` is larger or equal to 18', () => {
  const user = {
    "age": fest.number().min(18)
  }
  describe('when `approved` is `true`', () => {
    const approved = true
    it('should return `true`, () => {
      expect(isUserLegal(user, approved)).toBe(true)
    })
  })
  describe('when `approved` is `false`, () => {
    const approved = false
    it('should return `false`', () => {
       expect(isUserLegal(user, apprvoed)).toBe(true) 
    })
  })
})
describe('when `user.age` is lower than 18', () => {
  const user = {
    "age": fest.number().nonExclusiveMax(18)
  }
  describe('when `approved` is `true`', () => {
    const approved = true
    it('should return `false`, () => {
      expect(isUserLegal(user, approved)).toBe(true)
    })
  })
  describe('when `approved` is `false`, () => {
    const approved = false
    it('should return `false`', () => {
       expect(isUserLegal(user, apprvoed)).toBe(true) 
    })
  })
})
```

```ts
describe('when `user.age` is larger or equal to `18`', () => {
  const user = {
    "age": fest.number().min(18)
  }
  describe('when `approved` is `true`', () => {
    const approved = true
    it('should return `true`, () => {
      expect(isUserLegal(user, approved)).toBe(true)
    })
  })
  describe('when `approved` is `false`, () => {
    const approved = false
    it('should return `false`', () => {
       expect(isUserLegal(user, apprvoed)).toBe(true) 
    })
  })
})
describe('when `user.age` is lower than `18`', () => {
  const user = {
    "age": fest.number().nonExclusiveMax(18)
  }
  describe('when `approved` is `true`', () => {
    const approved = true
    it('should return `false`, () => {
      expect(isUserLegal(user, approved)).toBe(true)
    })
  })
  describe('when `approved` is `false`, () => {
    const approved = false
    it('should return `false`', () => {
       expect(isUserLegal(user, apprvoed)).toBe(true) 
    })
  })
})
```

## And logic (ChatGPT example)
https://chat.openai.com/c/cbd15926-2eda-44ea-b84d-893a5101d6f2

```ts
type User = {
  name: string
  age: number
}

const isUserAllowedEntry = (user: User, isOnList: boolean) => {
  if(user.age >= 18 && isOnList) {
    return true
  }
  return false
}
```

```json
{
  "functionName": "isUserAllowedEntry",
  "parameters": [
    {
      "name": "user",
      "type": "User",
      "properties": [
        {
          "name": "age",
          "type": "number"
        }
      ]
    },
    {
      "name": "onTheList",
      "type": "boolean"
    }
  ],
  "logic": [
    {
      "conditions": [
        {
          "parameter": "user.age",
          "comparison": ">= 18"
        },
        {
          "parameter": "onTheList",
          "value": true
        }
      ],
      "return": true
    },
    {
      "defaultReturn": false
    }
  ]
}
```

### More complex

```ts
type User = {
  name: string
  age: number
}

const isUserAllowedEntry = (user: User, nameList: string[]) => {
  if(user.age >= 18 && nameList.includes(name)) {
    return true
  }
  return false
}
```

```json
{
  "functionName": "isUserAllowedEntry",
  "parameters": [
    {
      "name": "user",
      "type": "User",
      "properties": [
        {
          "name": "name",
          "type": "string"
        },
        {
          "name": "age",
          "type": "number"
        }
      ]
    },
    {
      "name": "nameList",
      "type": "string[]"
    }
  ],
  "logic": [
    {
      "conditions": [
        {
          "parameter": "user.age",
          "comparison": ">= 18"
        },
        {
          "parameter": "user.name",
          "operation": "in",
          "listParameter": "nameList"
        }
      ],
      "return": true
    },
    {
      "defaultReturn": false
    }
  ]
}
```