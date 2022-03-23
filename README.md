# JavaScript-Calculator
// A Calculator using Javascript HTML and CSS //

function checkCashRegister(price, cash, register) {
  let change = {};
  change.status = "OPEN" ;
  change.change = [];

  let totalAmountInTheRegister =
  Math.round(register.reduce((acc, coin) => acc + coin[1], 0) * 100)/100;
  console.log("In Register", totalAmountInTheRegister);

  let amountDue = Math.round((cash - price)*100)/100;
  if (amountDue > totalAmountInTheRegister) {
  change.status = "INSUFFICIENT_FUNDS";
  return change;
}
if(totalAmountInTheRegister == amountDue) {
change.status = "CLOSED";
change.change = register;
return change;
}
const AMOUNTS = {
  "ONE HUNDRED": 100,
   TWENTY: 20,
   TEN: 10,
   FIVE: 5,
   ONE: 1,
   QUARTER: 0.25,
   DIME: 0.1,
   NICKEL: 0.05,
   PENNY: 0.01,
}
Object.keys(AMOUNTS).forEach((key) => {
  if(amountDue > AMOUNTS[key]) {
    let amountOfBillInTheRegister = 0;
    register.forEach((type) => {
      if(type[0] == key) {
        amountOfBillInTheRegister = type[1];
      }
    })
  
  let amountDueBefore = amountDue;
  amountDue = amountDue % AMOUNTS[key];
 amountDue = Math.round(amountDue *100)/100;
 let difference = Math.round((amountDueBefore - amountDue) * 100)/100;
  if(difference > amountOfBillInTheRegister) {
    change.change.push([key, amountOfBillInTheRegister])
    amountDue = amountDueBefore - amountOfBillInTheRegister;
  } else {
    change.change.push([key, difference])
  }
}
})
   if(amountDue > 0) {
     change.status = "INSUFFICIENT_FUNDS";
     change.change = [];
     return change;
   }

return change
}

checkCashRegister(19.5, 20, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.1], ["QUARTER", 4.25], ["ONE", 90], ["FIVE", 55], ["TEN", 20], ["TWENTY", 60], ["ONE HUNDRED", 100]]);


