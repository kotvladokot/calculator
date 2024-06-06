package main

import (
	"fmt"
	"os"
	"strconv"
	"strings"
	"unicode"
)

var romMap = map[string]int{
	"I": 1, "II": 2, "III": 3, "IV": 4, "V": 5, "VI": 6, "VII": 7, "VIII": 8, "IX": 9,
	"X": 10, "L": 50, "C": 100,
}

func romToara(roman string) int {
	return romMap[roman]
}

func arabicToRoman(arabic int) string {
	var result strings.Builder
	for arabic >= 100 {
		result.WriteString("C")
		arabic -= 100
	}
	if arabic >= 90 {
		result.WriteString("XC")
		arabic -= 90
	}
	for arabic >= 50 {
		result.WriteString("L")
		arabic -= 50
	}
	if arabic >= 40 {
		result.WriteString("XL")
		arabic -= 40
	}
	for arabic >= 10 {
		result.WriteString("X")
		arabic -= 10
	}
	if arabic == 9 {
		result.WriteString("IX")
		arabic -= 9
	}
	if arabic >= 5 {
		result.WriteString("V")
		arabic -= 5
	}
	if arabic == 4 {
		result.WriteString("IV")
		arabic -= 4
	}
	for arabic > 0 {
		result.WriteString("I")
		arabic -= 1
	}
	return result.String()
}
func isRom(input string) bool {
	for _, char := range input {
		if !unicode.IsLetter(char) || (unicode.ToUpper(char) != 'I' && unicode.ToUpper(char) != 'V' && unicode.ToUpper(char) != 'X') {
			return false
		}
	}
	return true
}
func pl(a int, b int) int {
	return a + b
}
func min(a int, b int) int {
	return a - b

}
func um(a int, b int) int {
	return a * b

}
func del(a int, b int) int {
	return a / b

}
func main() {

	for {
		fmt.Println("Введите пример через пробел:")
		fmt.Println("Для остановки работы программы в поле оператор введите s")

		var a, b string
		var s string
		var err = ""
		fmt.Fscanln(os.Stdin, &a, &s, &b, &err)
		if err != "" {
			panic("Памагите! пустой ввод!")
			return
		}
		if s == "s" {
			fmt.Println("Работа программы успешно завершена!Иди нахуй!")
			break
		}
		if isRom(a) != isRom(b) {
			panic("Не правильный ввод!")
			return
		}
		var numA, numB int
		if isRom(a) {
			numA = romToara(a)
		} else {
			numA, _ = strconv.Atoi(a)
		}
		if isRom(b) {
			numB = romToara(b)
		} else {
			numB, _ = strconv.Atoi(b)
		}
		var result int
		switch s {
		case "+":
			if numA < 0 && numA > 10 || numB < 0 || numB > 10 {
				panic("Ты втираешь мне какую то дичь!")
				return
			} else {
				result = pl(numA, numB)

			}
		case "-":
			if numA < 0 && numA > 10 || numB < 0 || numB > 10 {
				panic("Ты втираешь мне какую то дичь!")
				return

			} else {
				result = min(numA, numB)
			}

		case "*":
			if numA < 0 && numA > 10 || numB < 0 || numB > 10 {
				panic("Ты втираешь мне какую то дичь!")
				return
			} else {
				result = um(numA, numB)

			}

		case "/":
			if numA < 0 && numA > 10 || numB < 0 || numB > 10 {
				panic("Ты втираешь мне какую то дичь!")
				return
			} else {
				result = del(numA, numB)

			}

		default:
			panic("Не верный тип операции!")
			return

		}

		if isRom(a) && isRom(b) {
			var e = arabicToRoman(result)
			if e == "" {
				panic("Ошибка")
				return
			}
			fmt.Println("РЕзульат:", arabicToRoman(result))
		} else {
			fmt.Println("результат:", result)
		}
	}

}

