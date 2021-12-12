# Typescriptのimport export
Typescriptのimportは拡張子を指定しない。   
指定をすると不都合が発生する。

```
type Species = 'rabbit' | 'bear' | 'fox' | 'dog';

interface Resident { 
  name: string; 
  age: number; 
  species: Species;
}

const isCanine = (resident: Resident): boolean => 
  ['dog', 'fox'].includes(resident.species);

export { Species, Resident, isCanine };
```

```
const rate: { [unit: string]: number } = { 
  USD: 1,
  EUR: 0.9, 
  JPY: 108, 
  GBP: 0.8,
};

type Unit = keyof typeof rate; 
type Currency = {
  unit: Unit; 
  amount: number; 
};

const Currency = {
  exchange: (currency: Currency, unit: Unit): Currency => {
    const amount = currency.amount / rate[currency.unit] * rate[unit]; 

    return { unit, amount };
  }, 
};

export { Currency };
```
型エイリアスとオブジェクトは*同時に両方ともエクスポートされる*   
*コラボレーション*と言われている.   

```
import { Currency } from './currency-export.ts';

const dollars: Currency = {
  unit: 'USD';
  amount: 100;
};

console.log(dollars);
console.log(Currency.exchange(dollars, 'JPY'));

$ cd 04-typescript/05-advanced/module/ $ ts-node currency-import.ts
{ unit: "USD", amount: 100 }
{ unit: "JPY", amount: 10800 }
```
暗黙のうちに型とオブジェクトを同時にインポートする。   

```
type Species = 'rabbit' | 'bear' | 'fox' | 'dog';

class Resident {
  name = '';
  age = 0;
  species: Species | null = null;
}

export type { Species, Resident };
```

```
import { Resident } from './resident';
constresident = new Resident(); //compileerror! 
const patty: Resident = {
  name: 'Patty Rabbit', 
  age: 8,
  species: 'rabbit',
};

console.log(patty);
```

## JavascriptモジュールをTypescriptから読み込む

