<template>
  <div class="flex justify-center">
    <CurrencyConverter
      v-if="symbols && currencyValue"
      :symbols="symbols"
      :currencyValue="currencyValue"
    />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import CurrencyConverter from "@/components/currency-converter.vue";
import { ExchangeRateHostAPI } from "@/data";
import { Latest, SymbolType } from "@/domain";

@Component({
  components: {
    CurrencyConverter,
  },
})
export default class Home extends Vue {
  symbols: SymbolType | null = null;
  currencyValue: Latest | null = null;

  created(): void {
    ExchangeRateHostAPI.getSymbols().then((r) => {
      this.symbols = r.data.symbols;
    });

    ExchangeRateHostAPI.getLatest().then((r) => {
      this.currencyValue = r.data;
    });
  }
}
</script>
