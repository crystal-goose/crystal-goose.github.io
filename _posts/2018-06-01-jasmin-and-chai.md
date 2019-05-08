---
layout: base
title: Jasmin and chai
---

Jest use Jasmine as default. While in the Enzyme docs, it uses chai as default. So I list th difference between Jasmine and Chai here.

Jasmin ([Full reference](https://facebook.github.io/jest/docs/en/expect.html))
* toBe (Object.is under the hoodo)
* toEqual (value equal)
* not
    e.g. `expect(a + b).not.toBe(0)`
* toBeNull, toBeUndefined, toBeDefined, toBeTruthy, toBeFalsy
* toBeGreaterThan, toBeLessThan, toBeGreaterThanOrEqual, toBeLessThanOrEqual, toBeCloseTo
* toMatch (For Strings)
* toContain ( For arrays)
* toThrow (Exception)

Chai
```javascript
chai.should();
foo.should.be.a('string');
foo.should.equal('bar');
foo.should.have.lengthOf(3);
tea.should.have.property('flavors')
  .with.lengthOf(3);

var expect = chai.expect;

expect(foo).to.be.a('string');
expect(foo).to.equal('bar');
expect(foo).to.have.lengthOf(3);
expect(tea).to.have.property('flavors')
  .with.lengthOf(3);

var assert = chai.assert;

assert.typeOf(foo, 'string');
assert.equal(foo, 'bar');
assert.lengthOf(foo, 3)
assert.property(tea, 'flavors');
assert.lengthOf(tea.flavors, 3);
```


