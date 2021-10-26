O trigger é uma regra que é disparada quando alguma tabela sofre alteração nos seus dados, seja inclusão, exclusão ou alteração. Seria um gatilho.<br>
Pode ocorrer BEFORE ou AFTER, de um INSERT, UPDATE ou DELETE.<br>
Criamos um trigger com a seguinte sintaxe:
- AFTER INSERT
```
DELIMITER //
CREATE TRIGGER nomedocampo AFTER INSERT ON tabela
FOR EACH ROW
BEGIN
	comandos;
    comandos;
    comandos;
END //
```
- BEFORE INSERT
```
DELIMITER //
CREATE TRIGGER nomedocampo BEFORE INSERT ON tabela
FOR EACH ROW
BEGIN
	comandos;
    comandos;
    comandos;
END //
```
- AFTER UPDATE
```
DELIMITER //
CREATE TRIGGER nomedocampo AFTER UPDATE ON tabela
FOR EACH ROW
BEGIN
	comandos;
    comandos;
    comandos;
END //
```
- BEFORE UPDATE
```
DELIMITER //
CREATE TRIGGER nomedocampo BEFORE UPDATE ON tabela
FOR EACH ROW
BEGIN
	comandos;
    comandos;
    comandos;
END //
```
- AFTER DELETE
```
DELIMITER //
CREATE TRIGGER nomedocampo AFTER DELETE ON tabela
FOR EACH ROW
BEGIN
	comandos;
    comandos;
    comandos;
END //
```
- BEFORE DELETE
```
DELIMITER //
CREATE TRIGGER nomedocampo BEFORE DELETE ON tabela
FOR EACH ROW
BEGIN
	comandos;
    comandos;
    comandos;
END //
```