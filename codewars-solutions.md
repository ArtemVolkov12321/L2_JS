Первая задача

function hasTwoCubeSums(n) {
    const ways = [];
    const max = Math.floor(Math.cbrt(n));
    
    for (let a = 1; a <= max; a++) {
        for (let b = a + 1; b <= max; b++) {
            const sum = a * a * a + b * b * b;
            
            if (sum === n) {
                ways.push([a, b]);
            }
        }
    }
    
    if (ways.length < 2) {
        return false;
    }
    
    for (let i = 0; i < ways.length; i++) {
        for (let j = i + 1; j < ways.length; j++) {
            const [a1, b1] = ways[i];
            const [a2, b2] = ways[j];
            
            if (a1 !== a2 && a1 !== b2 && b1 !== a2 && b1 !== b2) {
                return true;
            }
        }
    }
    
    return false;
}

console.log(hasTwoCubeSums(1729)); // true
console.log(hasTwoCubeSums(42));   // false
console.log(hasTwoCubeSums(4104)); // true
console.log(hasTwoCubeSums(13832)); // true
console.log(hasTwoCubeSums(100));   // false

Вторая задача

function ipv4Parser(ip, subnet) {
    const ipParts = ip.split('.').map(Number);
    const subnetParts = subnet.split('.').map(Number);
    
    const network = ipParts.map((octet, i) => octet & subnetParts[i]);
    const host = ipParts.map((octet, i) => octet - network[i]);
    
    return [network.join('.'), host.join('.')];
}

Третья задача

function whatCentury(year) {
    const yearNum = parseInt(year);
    let century = Math.ceil(yearNum / 100);
    
    let suffix;
    if (century % 10 === 1 && century % 100 !== 11) {
        suffix = "st";
    } else if (century % 10 === 2 && century % 100 !== 12) {
        suffix = "nd";
    } else if (century % 10 === 3 && century % 100 !== 13) {
        suffix = "rd";
    } else {
        suffix = "th";
    }
    
    return century + suffix;
}

console.log(whatCentury("1999"));
console.log(whatCentury("2011"));
console.log(whatCentury("2154"));
console.log(whatCentury("2259"));
console.log(whatCentury("1124"));
console.log(whatCentury("2000"));

четвертая задача

function findMissing(list) {
    const step1 = list[1] - list[0];
    const step2 = list[list.length - 1] - list[list.length - 2];
    
    let step;
    if (Math.abs(step1) < Math.abs(step2)) {
        step = step1;
    } else {
        step = step2;
    }
    
    for (let i = 0; i < list.length - 1; i++) {
        if (list[i + 1] - list[i] !== step) {
            return list[i] + step;
        }
    }
    
    return list[0];
}

console.log(findMissing([1, 3, 5, 9, 11]));
console.log(findMissing([1, 5, 7, 9, 11]));
console.log(findMissing([1, 3, 7, 9, 11]));
console.log(findMissing([2, 4, 6, 10, 12]));
console.log(findMissing([10, 13, 16, 22, 25]));

пятая задача

function primeFactors(n) {
    let result = "";
    let temp = n;
    
    let count = 0;
    while (temp % 2 === 0) {
        temp /= 2;
        count++;
    }
    if (count > 0) {
        result += count === 1 ? "(2)" : `(2**${count})`;
    }
    
    for (let i = 3; i <= Math.sqrt(temp); i += 2) {
        count = 0;
        while (temp % i === 0) {
            temp /= i;
            count++;
        }
        if (count > 0) {
            result += count === 1 ? `(${i})` : `(${i}**${count})`;
        }
    }
    
    if (temp > 1) {
        result += `(${temp})`;
    }
    
    return result;
}

console.log(primeFactors(86240));
console.log(primeFactors(7775460));
console.log(primeFactors(7919));
console.log(primeFactors(17));
console.log(primeFactors(8));
console.log(primeFactors(12));

шестая задача

function toWeirdCase(string) {
    return string.split(' ')
                 .map(word => 
                     word.split('')
                         .map((char, index) => 
                             index % 2 === 0 ? char.toUpperCase() : char.toLowerCase()
                         )
                         .join('')
                 )
                 .join(' ');
}

console.log(toWeirdCase("String"));
console.log(toWeirdCase("Weird string case"));
console.log(toWeirdCase("This is a test"));
console.log(toWeirdCase("ABCD"));
console.log(toWeirdCase("a"));
console.log(toWeirdCase("ab"));
