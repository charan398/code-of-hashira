function findConstantTerm(points) {
    let result = 0;
    
    for (let i = 0; i < points.length; i++) {
        let term = Number(points[i].y);
        
        for (let j = 0; j < points.length; j++) {
            if (i !== j) {
                term *= (-Number(points[j].x)) / (Number(points[i].x) - Number(points[j].x));
            }
        }
        result += term;
    }
    return Math.round(result);
}

const toDecimal = (value, base) => BigInt(parseInt(value, base));

const testCase1 = {
    "keys": { "n": 4, "k": 3 },
    "1": { "base": "10", "value": "4" },
    "2": { "base": "2", "value": "111" },
    "3": { "base": "10", "value": "12" },
    "6": { "base": "4", "value": "213" }
};

const testCase2 = {
    "keys": { "n": 10, "k": 7 },
    "1": { "base": "6", "value": "13444211440455345511" },
    "2": { "base": "15", "value": "aed7015a346d635" },
    "3": { "base": "15", "value": "6aeeb69631c227c" },
    "4": { "base": "16", "value": "e1b5e05623d881f" },
    "5": { "base": "8", "value": "316034514573652620673" },
    "6": { "base": "3", "value": "2122212201122002221120200210011020220200" },
    "7": { "base": "3", "value": "20120221122211000100210021102001201112121" },
    "8": { "base": "6", "value": "20220554335330240002224253" },
    "9": { "base": "12", "value": "45153788322a1255483" },
    "10": { "base": "7", "value": "1101613130313526312514143" }
};

function solve(testData) {
    const { k } = testData.keys;
    const points = Object.keys(testData)
        .filter(key => key !== 'keys')
        .map(key => ({
            x: parseInt(key),
            y: toDecimal(testData[key].value, parseInt(testData[key].base))
        }))
        .sort((a, b) => a.x - b.x)
        .slice(0, k);
    return findConstantTerm(points);
}

const c1 = solve(testCase1);
const c2 = solve(testCase2);

console.log(c1);
console.log(c2);