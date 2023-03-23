<template>
  <div
    style="
      width: 100vw;
      display: flex;
      justify-content: center;
      align-items: center;
    "
  >
    <table border>
      <thead>
        <tr>
          
          <th>Input Numberical Value</th>
          <th>Input Unit of Measure</th>
          <th>Target Unit of Measure</th>
          <th>Student Responce</th>
          <th>Output</th>
        </tr>
      </thead>
      <tbody>
        <template v-for="(data, indx) in tableData" :key="indx">
          <tr>
            <td>
              <input
                type="number"
                v-model="data.qstValue"
                @input="hanldeResponce(data, indx)"
              />
            </td>
            <td>
              <input type="text" v-model="data.fromUint" />
            </td>
            <td>
              <input type="text" v-model="data.toUnit" />
            </td>
            <td>
              <input
                type="number"
                v-model="data.stdntResponce"
                @input="hanldeResponce(data, indx)"
              />
            </td>
            <td style="padding: 0 5px">{{ data.Output }}</td>
          </tr>
        </template>
      </tbody>
    </table>
  </div>
</template>

<script>
import { isProxy, toRaw } from "vue";
export default {
  name: "ConvCalculator",
 

  mounted() {
    this.callInitialTableData();
  },
  data() {
    return {
      tableData: null,
      unitsOfTemprature: {
        kalvin: "kalvin",
        calsius: "calsius",
        fahrenheit: "fahrenheit",
        rankine: "rankine",
      },
      unitsOfVolume: {
        liters: "liters",
        tablespoons: "tablespoons",
        cubicinches: "cubicinches",
        cups: "cups",
        cubicfeet: "cubicfeet",
        gallons: "gallons",
      },
    };
  },
  methods: {
    callInitialTableData() {
      this.tableData = [
        {
          qstValue: null,
          fromUint: "",
          toUnit: "",
          stdntResponce: null,
          Output: "",
        },
        {
          qstValue: null,
          fromUint: "",
          toUnit: "",
          stdntResponce: null,
          Output: "",
        },
        {
          qstValue: null,
          fromUint: "",
          toUnit: "",
          stdntResponce: null,
          Output: "",
        },
        {
          qstValue: null,
          fromUint: "",
          toUnit: "",
          stdntResponce: null,
          Output: "",
        },
        {
          qstValue: null,
          fromUint: "",
          toUnit: "",
          stdntResponce: null,
          Output: "",
        },
        {
          qstValue: null,
          fromUint: "",
          toUnit: "",
          stdntResponce: null,
          Output: "",
        },
      ];
    },

    truncatValueUpToTen(value) {
      let num = Number(value);
      if (isNaN(num)) {
        return null;
      }

      return num;
    },
    hanldeResponce(rowData, indx) {
      const { unitsOfTemprature, unitsOfVolume } = this;

      let data = rowData;
      let tableData = [...this.tableData];

      if (isProxy(data)) data = toRaw(data);
      // if (isProxy(this.tableData)) this.tableData = toRaw(this.tableData);

      let answer = null;

      let valueOfQuestion = this.truncatValueUpToTen(data.qstValue);
      let studentResponce = this.truncatValueUpToTen(data.stdntResponce);

      let kelvin;

      if (
        unitsOfTemprature[data.fromUint] &&
        unitsOfTemprature[data.toUnit] &&
        !isNaN(studentResponce)
      ) {

        switch (data.fromUint != null) {
          // calsius -------->
          case data.fromUint === "calsius":
            switch (data.toUnit != null) {
              //calcius to calcius
              case data.fromUint === data.toUnit:
                data.Output =
                  valueOfQuestion === studentResponce ? "Correct" : "Incorrect";
                break;

              //calcius to kalvin
              case data.toUnit === "kalvin":
                answer = this.truncatValueUpToTen(valueOfQuestion + 273.15);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              //calcius to fahrenheit
              case data.toUnit === "fahrenheit":
                answer = this.truncatValueUpToTen(valueOfQuestion * 1.8 + 32);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              //calcius to rankine
              case data.toUnit === "rankine":
                kelvin = valueOfQuestion + 273.15;
                answer = this.truncatValueUpToTen(kelvin * 1.8);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              default:
                answer = null;
                data.Output = "";
                break;
            }
            break;

          // fahrenheit -------->
          case data.fromUint === "fahrenheit":
            switch (data.toUnit != null) {
              //fahrenheit to fahrenheit
              case data.fromUint === data.toUnit:
                data.Output =
                  valueOfQuestion === studentResponce ? "Correct" : "Incorrect";
                break;

              //fahrenheit to kalvin
              case data.toUnit === "kalvin":
                answer = this.truncatValueUpToTen(
                  (valueOfQuestion - 32) * (5 / 9) + 273.15
                );
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              //fahrenheit to calsius
              case data.toUnit === "calsius":
                answer = this.truncatValueUpToTen(
                  (valueOfQuestion - 32) * (5 / 9)
                );
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              //fahrenheit to rankine
              case data.toUnit === "rankine":
                answer = this.truncatValueUpToTen(valueOfQuestion + 459.67);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              default:
                answer = null;
                data.Output = "";
                break;
            }
            break;

          // rankine -------->
          case data.fromUint === "rankine":
            switch (data.toUnit != null) {
              //rankine to rankine
              case data.fromUint === data.toUnit:
                data.Output =
                  valueOfQuestion === studentResponce ? "Correct" : "Incorrect";
                break;

              //rankine to kalvin
              case data.toUnit === "kalvin":
                answer = this.truncatValueUpToTen(
                  ((valueOfQuestion - 491.67) * 5) / 9
                );
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              //rankine to calsius
              case data.toUnit === "calsius":
                answer = this.truncatValueUpToTen(
                  ((valueOfQuestion - 491.67) * 5) / 9 - 273.15
                );
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              //rankine to fahrenheit
              case data.toUnit === "fahrenheit":
                answer = this.truncatValueUpToTen(valueOfQuestion - 459.67);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              default:
                answer = null;
                data.Output = "";
                break;
            }
            break;
          // kalvin -------->
          case data.fromUint === "kalvin":
            switch (data.toUnit != null) {
              //kalvin to kalvin
              case data.fromUint === data.toUnit:
                data.Output =
                  valueOfQuestion === studentResponce ? "Correct" : "Incorrect";
                break;

              //kalvin to rankine
              case data.toUnit === "rankine":
                answer = this.truncatValueUpToTen(valueOfQuestion * 1.8);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              //kalvin to calsius
              case data.toUnit === "calsius":
                answer = this.truncatValueUpToTen(valueOfQuestion - 273.15);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              //kalvin to fahrenheit
              case data.toUnit === "fahrenheit":
                kelvin = (valueOfQuestion - 273.15) * 1.8 + 32;
                answer = this.truncatValueUpToTen(kelvin * 1.8);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              default:
                answer = null;
                data.Output = "";
                break;
            }
            break;

          default:
            answer = null;
            data.Output = "";
            break;
        }

        //volume ------->
      } else if (
        unitsOfVolume[data.fromUint] &&
        unitsOfVolume[data.toUnit] &&
        !isNaN(studentResponce)
      ) {
        switch (data.fromUint != null) {
          // liters
          case data.fromUint === "liters":
            switch (data.toUnit != null) {
              // liters to liters
              case data.fromUint === data.toUnit:
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              // liters to tablespoons
              case data.toUnit === "tablespoons":
                answer = this.truncatValueUpToTen(valueOfQuestion * 67.628);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              // liters to cubicinches
              case data.toUnit === "cubicinches":
                answer = this.truncatValueUpToTen(valueOfQuestion * 61.024);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              // liters to cups
              case data.toUnit === "cups":
                answer = this.truncatValueUpToTen(valueOfQuestion * 4.22675);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";

                break;
              // liters to cubicfeet
              case data.toUnit === "cubicfeet":
                answer = this.truncatValueUpToTen(valueOfQuestion * 0.0353147);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              // liters to gallon
              case data.toUnit === "gallons":
                answer = this.truncatValueUpToTen(valueOfQuestion * 0.264172);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              default:
                answer = null;
                data.Output = "";
                break;
            }
            break;

          // tablespoons
          case data.fromUint === "tablespoons":
            switch (data.toUnit != null) {
              // tablespoons to tablespoons
              case data.fromUint === data.toUnit:
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              // tablespoons to liters
              case data.toUnit === "liters":
                answer = this.truncatValueUpToTen(valueOfQuestion * 0.0147868);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              // tablespoons to cubicinches
              case data.toUnit === "cubicinches":
                answer = this.truncatValueUpToTen(valueOfQuestion * 0.902344);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              // tablespoons to cups
              case data.toUnit === "cups":
                answer = this.truncatValueUpToTen(valueOfQuestion / 16);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              // tablespoons to cubicfeet
              case data.toUnit === "cubicfeet":
                answer = this.truncatValueUpToTen(valueOfQuestion / 1915.013);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              // tablespoons to gallons
              case data.toUnit === "gallons":
                answer = this.truncatValueUpToTen(valueOfQuestion / 256);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              default:
                answer = null;
                data.Output = "";
                break;
            }
            break;
          //cubicinches
          case data.fromUint === "cubicinches":
            switch (data.toUnit != null) {
              //cubicinches to cubicinches
              case data.fromUint === data.toUnit:
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //cubicinches to tablesspoons
              case data.toUnit === "tablespoons":
                answer = this.truncatValueUpToTen(valueOfQuestion * 1.10823);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //cubicinches to liters
              case data.toUnit === "liters":
                answer = this.truncatValueUpToTen(
                  valueOfQuestion * 0.016387064
                );
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //cubicinches to cups
              case data.toUnit === "cups":
                answer = this.truncatValueUpToTen(
                  valueOfQuestion * 0.0692640693
                );
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //cubicinches to cubicfeet
              case data.toUnit === "cubicfeet":
                answer = this.truncatValueUpToTen(
                  valueOfQuestion * 0.000578704
                );
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //cubicinches to gallons
              case data.toUnit === "gallons":
                answer = this.truncatValueUpToTen(valueOfQuestion / 231);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              default:
                answer = null;
                data.Output = "";
                break;
            }
            break;
          // cups ---- >
          case data.fromUint === "cups":
            switch (data.toUnit != null) {
              //cups to cups
              case data.fromUint === data.toUnit:
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //cups to tablespoons
              case data.toUnit === "tablespoons":
                answer = this.truncatValueUpToTen(valueOfQuestion * 16);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //cups to cubicinches
              case data.toUnit === "cubicinches":
                answer = this.truncatValueUpToTen(valueOfQuestion * 14.4375);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //cups to liters
              case data.toUnit === "liters":
                answer = this.truncatValueUpToTen(valueOfQuestion * 0.236588);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //cups to cubicfeet
              case data.toUnit === "cubicfeet":
                answer = this.truncatValueUpToTen(valueOfQuestion / 256);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //cups to gallons
              case data.toUnit === "gallons":
                answer = this.truncatValueUpToTen(valueOfQuestion * 0.0625);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              default:
                answer = null;
                data.Output = "";
                break;
            }
            break;
          // cubicfeet
          case data.fromUint === "cubicfeet":
            switch (data.toUnit != null) {
              //cubicfeet to cubicfeet
              case data.fromUint === data.toUnit:
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //cubicfeet to tablespoons
              case data.toUnit === "tablespoons":
                answer = this.truncatValueUpToTen(valueOfQuestion * 1728 * 0.5);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //cubicfeet to cubicinches
              case data.toUnit === "cubicinches":
                answer = this.truncatValueUpToTen(valueOfQuestion * 1728);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //cubicfeet to cups
              case data.toUnit === "cups":
                answer = this.truncatValueUpToTen(valueOfQuestion * 119.688);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              case data.toUnit === "liters":
                answer = valueOfQuestion / 256;
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //cubicfeet to gallons
              case data.toUnit === "gallons":
                answer = this.truncatValueUpToTen(valueOfQuestion * 7.48052);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              default:
                answer = null;
                data.Output = "";
                break;
            }
            break;
          //gallons
          case data.fromUint === "gallons":
            switch (data.toUnit != null) {
              //gallons to gallons
              case data.fromUint === data.toUnit:
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //gallons to tablespoons
              case data.toUnit === "tablespoons":
                answer = this.truncatValueUpToTen(valueOfQuestion * 256);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //gallons to cubicinches
              case data.toUnit === "cubicinches":
                answer = this.truncatValueUpToTen(valueOfQuestion * 231);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //gallons to cups
              case data.toUnit === "cups":
                answer = this.truncatValueUpToTen(valueOfQuestion * 16);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //gallons to cubicfeet
              case data.toUnit === "cubicfeet":
                answer = this.truncatValueUpToTen(valueOfQuestion * 0.133681);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;
              //gallons to liters
              case data.toUnit === "liters":
                answer = this.truncatValueUpToTen(valueOfQuestion * 3.78541);
                data.Output =
                  answer === studentResponce ? "Correct" : "Incorrect";
                break;

              default:
                answer = null;
                data.Output = "";
                break;
            }
            break;

          default:
            answer = null;
            data.Output = "";
            break;
        }
      } else {
        data.Output = "Invalid";
        console.log("Invalid Conversion");
      }
      tableData[indx] = data;
      this.tableData = tableData;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

input {
  border: none;
  outline: none;
  font-size: 12px;
}

th {
  padding: 10px;
}

input:focus {
  border: none;
}
</style>
