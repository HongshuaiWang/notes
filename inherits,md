#### javascript继承
   
```
//创建对象
var beget = function (o) {
    var F = function () {
    };
    if (typeof o === 'object') {
        F.prototype = o;
    }
    return new F();
};
  
var findSuper = function (obj, n, method) {
    var index = obj.super.fn.length - n;
    if (index < 0) {
        return null;
    }
    return obj.super.fn[index][method];
};
  
window.inherits = function (subType, superType) {
    if (subType) {
        var prototype = beget(superType.prototype);
        prototype.constructor = subType;
        subType.prototype = prototype;
        if (subType.prototype.super) {
            if (!subType.prototype.super.fn) {
                console.log(new Error('super error invalid super'));
            }
            subType.prototype.super.fn.push(superType.prototype);
            return;
        } else {
            var superCall = {};
            subType.prototype.super = function (method) {
                if (superCall.hasOwnProperty(method)) {
                    superCall[method]++;
                } else {
                    superCall[method] = 1;
                }
                var n = superCall[method];
                var f = findSuper(this, n, method);
                if (!f) throw new Error('super error no method');
                var slice = Array.prototype.slice;
                var args = slice.call(arguments, 1);
                try {
                    return f.apply(this, args);
                } finally {
                    superCall[method] = 0;
                }
            };
            subType.prototype.super.fn = [superType.prototype]
        }
    }
}
```
  
  
###### 使用方式
```
function People(name, age) {
    this.name = name;
    this.age = age;
}
  
People.prototype.introduce = function () {
    console.log(`My name is ${this.name}, I am ${this.age} years old`);
}
  
  
  
function Male(name, age) {
    People.call(this, name, age);
}

inherits(Male, People);  
  
Male.prototype.introduce = function () {
    this.super('introduce');
    console.log(`I am a man`);
}
  
  
  
function Female(name, age) {
    People.call(this, name, age);
}

inherits(Female, People);
  
  
  
function MaleModel(name, age) {
    Male.call(this, name, age);
}
  
inherits(MaleModel, Male);
  
MaleModel.prototype.introduce = function () {
    this.super('introduce');
    console.log(`My job is model`);
}
    
```
