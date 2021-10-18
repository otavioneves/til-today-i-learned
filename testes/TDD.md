O TDD, Test-Driven-Development, ou Desenvolvimento Guiado pelos Testes, é uma metodologia aonde fazemos os testes antes da implementação. A idéia é que você faça um teste e depois vá para a aplicação fazer o código que funcionaria para aquele teste. Após ter terminado, voltamos para os testes e fazer o próximo cenário, depois a próxima implementação no código ou refatoração, e assim suscetivamente. Nessa metodologia verificamos o comportamento antes de implementá-lo.<br>
Uma das grandes vantagens é que ao fazer o refactoring, garantimos que o funcionamento estará ok se o novo código refatorado passar nos testes, dando maior tranquilidade para executar melhorias no código. As vantagens do TDD são:
- O código ao ser feito através do TDD já sai testado;
- Evitamos testes "viciados", onde escreveríamos o teste com a implementação que já criamos anteriormente, o que é errado pois o teste tem que ser voltado para o comportamento e não pela implementação, pois o comportamento é independente da implementação.;
- Refatoração mais constante, aumentando a qualidade do código;
- Te ajuda a manter o foco;
- Temos uma tendência em escrever um código mais simples.
O ideal é utilizar TDD é quando a aplicação será complexa, ou o código é diferente do que é feito no dia a dia, com regras, etc. aonde não sabemos exatamente como o código irá ficar. Quando o código é muito trivial, feito diariamente, não tenha necessidade de utilizar o TDD, por ja conhecer muito bem o funcionamento.<br>
Da mesma maneira que refatoramos o código, também é uma boa prática refatorar os códigos do teste, a fim de deixar ele sempre atualizado e sempre manutenível.