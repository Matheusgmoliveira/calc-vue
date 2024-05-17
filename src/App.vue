<script setup>
import {reactive, watch} from 'vue';

const calculadora= reactive({
    filtro:'somar',
    num1:0,
    num2:0,
    resultado:0
  
})


const funcaoSomar = () => {
  const somar = parseFloat(calculadora.num1) + parseFloat(calculadora.num2);
  calculadora.resultado = somar;
}

const funcaoMultiplicar = () => {
  const multiplicar = parseFloat(calculadora.num1) * parseFloat(calculadora.num2);
  calculadora.resultado = multiplicar;
}

const funcaoDividir = () => {
  if (calculadora.num2 != 0) {
    const dividir = parseFloat(calculadora.num1) / parseFloat(calculadora.num2);
    calculadora.resultado = dividir;
  } else {
    calculadora.resultado = 'Erro: Divisão por zero';
  }
}

const funcaoSubtrair = () => {
  const subtrair = parseFloat(calculadora.num1) - parseFloat(calculadora.num2);
  calculadora.resultado = subtrair;
}

const operador = () =>{
  const{filtro} = calculadora;
  switch(filtro){
    case 'somar':
      return funcaoSomar();
    case 'multiplicar':
      return funcaoMultiplicar();
    case 'dividir':
      return funcaoDividir();
    case 'subtrair':
      return funcaoSubtrair();
    default:
      return 0
  }
}

const calcular = () =>{
  operador();
}

watch ( () => [calculadora.num1, calculadora.num2, calculadora.filtro],calcular)
</script>

<template>
  <div class="container">
    <h1 class="p-5 mb-4 mt-4 bg-light rounded-3">Calculadora</h1>
    <div class="row">
      <div class="col-md-3">
        <input @keyup ="evento => calculadora.num1 = evento.target.value" type="number" name="" id="" class="form-control">
      </div>
      <div class="col-md-3">
        <input @keyup ="evento => calculadora.num2 = evento.target.value" type="number" name="" id="" class="form-control">
      </div>
      <div class="col-md-3">
        <select  @change ="evento =>calculadora.filtro=evento.target.value"class="form-control">
          <option value="somar">Somar</option>
          <option value="multiplicar">Multiplicar</option>
          <option value="subtrair">Subtrair</option>
          <option value="dividir">Dividir</option>
        </select>
      </div>
      
      <div class="row">
        <div class="mt-3 col-md-2">
          <p class="form-control" >{{ calculadora.resultado }}</p>
          
        </div>
        
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
