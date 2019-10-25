---
title: 산술 연산자 - C# 참조
description: 숫자 형식이 포함된 곱하기, 나누기, 나머지, 더하기 및 빼기 작업을 수행하는 C# 연산자에 대해 알아봅니다.
ms.date: 03/27/2019
author: pkulikov
f1_keywords:
- ++_CSharpKeyword
- --_CSharpKeyword
- '*_CSharpKeyword'
- /_CSharpKeyword
- '%_CSharpKeyword'
- +_CSharpKeyword
- -_CSharpKeyword
helpviewer_keywords:
- arithmetic operators [C#]
- increment operator [C#]
- ++ operator [C#]
- decrement operator [C#]
- -- operator [C#]
- multiplication operator [C#]
- '* operator [C#]'
- division operator [C#]
- / operator [C#]
- remainder operator [C#]
- '% operator [C#]'
- addition operator [C#]
- + operator [C#]
- subtraction operator [C#]
- '- operator [C#]'
ms.openlocfilehash: ac04ba72ed0c25aa576bf10150fc80410890eda0
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69608374"
---
# <a name="arithmetic-operators-c-reference"></a>산술 연산자(C# 참조)

다음 연산자는 숫자 형식을 포함한 산술 작업을 수행합니다.

- 단항 [`++`(증분)](#increment-operator-), [`--`(감소)](#decrement-operator---), [`+`(더하기)](#unary-plus-and-minus-operators), [`-`(빼기)](#unary-plus-and-minus-operators) 연산자
- 이진 [`*`(곱하기)](#multiplication-operator-), [`/`(나누기)](#division-operator-), [`%`(나머지)](#remainder-operator-), [`+`(더하기)](#addition-operator-) 및 [`-`(빼기)](#subtraction-operator--) 연산자

해당 연산자는 모든 [정수](../builtin-types/integral-numeric-types.md) 및 [부동 소수점](../builtin-types/floating-point-numeric-types.md) 숫자 형식을 지원합니다.

## <a name="increment-operator-"></a>증가 연산자 ++

단항 증가 연산자(`++`)는 피연산자를 1씩 증가합니다. 피연산자는 변수, [속성](../../programming-guide/classes-and-structs/properties.md) 액세스 또는 [인덱서](../../programming-guide/indexers/index.md) 액세스여야 합니다.

증가 연산자는 후위 증가 연산자 `x++` 및 전위 증가 연산자 `++x`라는 두 가지 양식으로 지원됩니다.

### <a name="postfix-increment-operator"></a>후위 증가 연산자

`i++`의 결과는 다음 예제와 같이 연산 ‘전’ `i`의 값입니다. 

[!code-csharp-interactive[postfix increment](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#PostfixIncrement)]

### <a name="prefix-increment-operator"></a>전위 증가 연산자

`++a`의 결과는 다음 예제와 같이 연산 ‘후’ `a`의 값입니다. 

[!code-csharp-interactive[prefix increment](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#PrefixIncrement)]

## <a name="decrement-operator---"></a>감소 연산자 --

단항 감소 연산자(`--`)는 피연산자를 1씩 감소합니다. 피연산자는 변수, [속성](../../programming-guide/classes-and-structs/properties.md) 액세스 또는 [인덱서](../../programming-guide/indexers/index.md) 액세스여야 합니다.

감소 연산자는 후위 감소 연산자 `x--` 및 전위 감소 연산자 `--x`라는 두 가지 양식으로 지원됩니다.

### <a name="postfix-decrement-operator"></a>후위 감소 연산자

`i--`의 결과는 다음 예제와 같이 연산 ‘전’ `i`의 값입니다. 

[!code-csharp-interactive[postfix decrement](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#PostfixDecrement)]

### <a name="prefix-decrement-operator"></a>전위 감소 연산자

`--a`의 결과는 다음 예제와 같이 연산 ‘후’ `a`의 값입니다. 

[!code-csharp-interactive[prefix decrement](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#PrefixDecrement)]

## <a name="unary-plus-and-minus-operators"></a>단항 더하기 및 빼기 연산자

단항 `+` 연산자는 피연산자의 값을 반환합니다. 단항 `-` 연산자는 피연산자의 숫자 부정을 계산합니다.

[!code-csharp-interactive[unary plus and minus](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#UnaryPlusAndMinus)]

단항 `-` 연산자는 [ulong](../builtin-types/integral-numeric-types.md) 형식을 지원하지 않습니다.

## <a name="multiplication-operator-"></a>곱하기 연산자 *

곱하기 연산자 `*`는 피연산자의 곱을 계산합니다.

[!code-csharp-interactive[multiplication operator](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#Multiplication)]

단항 `*` 연산자는 [포인터 간접 참조 연산자](pointer-related-operators.md#pointer-indirection-operator-)입니다.

## <a name="division-operator-"></a>나누기 연산자 /

나누기 연산자 `/`는 오른쪽 피연산자로 왼쪽 피연산자를 나눕니다.

### <a name="integer-division"></a>정수 나누기

정수 형식의 피연산자의 경우 `/` 연산자의 결과는 정수 형식이고 두 피연산자의 몫과 동일한 값은 0으로 반올림됩니다.

[!code-csharp-interactive[integer division](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#IntegerDivision)]

두 피연산자의 몫을 부동 소수점 숫자로 가져오려면 `float`, `double` 또는 `decimal` 형식을 사용하세요.

[!code-csharp-interactive[integer as floating-point division](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#IntegerAsFloatingPointDivision)]

### <a name="floating-point-division"></a>부동 소수점 나누기

`float`, `double` 및 `decimal` 형식의 경우 `/` 연산자의 결과는 두 피연산자의 몫입니다.

[!code-csharp-interactive[floating-point division](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#FloatingPointDivision)]

피연산자 중 하나가 `decimal`이면 `float` 또는 `double` 모두 `decimal`로 암시적으로 변환할 수 없기 때문에 나머지 피연산자는 `float` 또는 `double`일 수 없습니다. `float` 또는 `double` 피연산자를 `decimal` 형식으로 암시적으로 변환해야 합니다. 숫자 형식 간의 암시적 변환에 대한 자세한 내용은 [암시적 숫자 변환 표](../keywords/implicit-numeric-conversions-table.md)를 참조하세요.

## <a name="remainder-operator-"></a>나머지 연산자 %

나머지 연산자 `%`는 왼쪽 피연산자를 오른쪽 피연산자로 나눈 후 나머지를 계산합니다.

### <a name="integer-remainder"></a>정수 나머지
  
정수 형식의 피연산자의 경우 `a % b`의 결과가 `a - (a / b) * b`에서 생성된 값입니다. 다음 예와 같이 0이 아닌 나머지의 부호는 왼쪽 피연산자와 동일합니다.

[!code-csharp-interactive[integer remainder](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#IntegerRemainder)]

<xref:System.Math.DivRem%2A?displayProperty=nameWithType> 메서드를 사용하여 정수 나누기 및 나머지 결과를 모두 컴퓨팅합니다.

### <a name="floating-point-remainder"></a>부동 소수점 나머지

`float` 및 `double` 피연산자의 경우 유한 `x` 및 `y`에 대한 `x % y`의 결과는 다음과 같은 `z` 값입니다.

- 0이 아닌 경우 `z`의 부호는 `x`의 부호와 동일합니다.
- `z`의 절대 값은 `|x| - n * |y|`에서 생성된 값입니다. 여기서 `n`은 `|x| / |y|`보다 작거나 같은 가능한 최대 정수이고 `|x|` 및 `|y|`는 각각 `x` 및 `y`의 절대 값입니다.

> [!NOTE]
> 나머지 계산 방법은 정수 피연산자에 사용되는 것과 유사하지만 IEEE 754와는 다릅니다. IEEE 754를 준수하는 나머지 작업이 필요한 경우 <xref:System.Math.IEEERemainder%2A?displayProperty=nameWithType> 메서드를 사용합니다.

무한 피연산자가 있는 `%` 연산자의 동작에 대한 자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [나머지 연산자](~/_csharplang/spec/expressions.md#remainder-operator) 섹션을 참조하세요.

`decimal` 피연산자의 경우 나머지 연산자 `%`는 <xref:System.Decimal?displayProperty=nameWithType> 형식의 [나머지 연산자](<xref:System.Decimal.op_Modulus(System.Decimal,System.Decimal)>)와 동일합니다.

다음 예제에서는 부동 소수점 피연산자를 포함한 나머지 연산자의 동작을 보여줍니다.

[!code-csharp-interactive[floating-point remainder](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#FloatingPointRemainder)]

## <a name="addition-operator-"></a>더하기 연산자 +

더하기 연산자 `+`는 피연산자의 합계를 계산합니다.

[!code-csharp-interactive[addition operator](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#Addition)]

문자열 연결 및 대리자 조합의 경우 `+` 연산자를 사용할 수도 있습니다. 자세한 내용은 참조는 [`+` 및 `+=`연산자](addition-operator.md) 문서를 참조하세요.

## <a name="subtraction-operator--"></a>빼기 연산자 -

빼기 연산자 `-`는 왼쪽 피연산자에서 오른쪽 피연산자를 뺍니다.

[!code-csharp-interactive[subtraction operator](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#Subtraction)]

대리자 제거의 경우 `-` 연산자를 사용할 수도 있습니다. 자세한 내용은 [`-` 연산자](subtraction-operator.md) 문서를 참조하세요.

## <a name="compound-assignment"></a>복합 할당

이진 연산자(`op`)의 경우 양식의 복합 할당 식

```csharp
x op= y
```

위의 식은 아래의 식과 동일합니다.

```csharp
x = x op y
```

단, `x`가 한 번만 계산됩니다.

다음 예제에서는 산술 연산자를 사용하는 복합 할당의 사용법을 보여줍니다.

[!code-csharp-interactive[compound assignment](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#CompoundAssignment)]

[숫자 승격](~/_csharplang/spec/expressions.md#numeric-promotions)으로 인해 `op` 연산의 결과가 암시적으로 `x`의 `T` 형식으로 변환되지 못할 수 있습니다. 이 경우 `op`가 미리 정의된 연산자이고 연산의 결과가 명시적으로 `x`의 `T` 형식으로 변환 가능하다면 `x op= y` 양식의 복합 할당 식이 `x = (T)(x op y)`에 해당합니다. 단 `x`는 한 번만 평가됩니다. 다음 예제에서는 해당 동작을 보여줍니다.

[!code-csharp-interactive[compound assignment with cast](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#CompoundAssignmentWithCast)]

`+=` 및 `-=` 연산자를 사용하여 [이벤트](../keywords/event.md)에서 구독하거나 구독을 취소할 수도 있습니다. 자세한 내용은 [방법: 이벤트 구독 및 구독 취소](../../programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)를 참조하세요.

## <a name="operator-precedence-and-associativity"></a>연산자 우선 순위 및 결합성

다음 목록에서는 산술 연산자를 가장 높은 우선 순위부터 가장 낮은 것으로 정렬합니다.

- 후위 증가 `x++` 및 감소 `x--` 연산자
- 전위 증가 `++x` 및 감소 `--x` 및 단항 `+` 및 `-` 연산자
- 곱하기 `*`, `/` 및 `%` 연산자
- 가감 `+` 및 `-` 연산자

이진 산술 연산자는 왼쪽 결합형입니다. 즉, 우선 순위 수준이 같은 연산자는 왼쪽에서 오른쪽으로 계산됩니다.

괄호(`()`)를 사용하여 연산자 우선 순위와 연결에 따라 주어진 계산 순서를 변경할 수 있습니다.

[!code-csharp-interactive[precedence and associativity](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#PrecedenceAndAssociativity)]

우선 순위 수준에 따라 정렬된 전체 연산자 목록은 [C# 연산자](index.md)를 참조하세요.

## <a name="arithmetic-overflow-and-division-by-zero"></a>산술 오버플로 및 0으로 나누기

산술 연산의 결과가 관련된 숫자 형식의 가능한 유한 값 범위를 벗어나는 경우 산술 연산자의 동작은 해당하는 피연산자의 형식에 따라 달라집니다.

### <a name="integer-arithmetic-overflow"></a>정수 산술 오버플로

정수를 0으로 나누면 항상 <xref:System.DivideByZeroException>이 throw됩니다.

정수 산술 오버플로의 경우 [checked 또는 unchecked](../keywords/checked-and-unchecked.md)일 수 있는 오버플로 검사 컨텍스트는 결과 동작을 제어합니다.

- checked 컨텍스트인 경우 상수 식에서 오버플로가 일어나면 컴파일 시간 오류가 발생합니다. 그렇지 않으면, 런타임 시 작업을 수행하는 경우 <xref:System.OverflowException>이 throw됩니다.
- unchecked 컨텍스트에서는 대상 형식에 맞지 않는 상위 비트를 버려서 해당 결과가 잘려집니다.

[checked 및 unchecked](../keywords/checked-and-unchecked.md) 문과 함께 `checked` 및 `unchecked` 연산자를 사용하여 식을 계산하는 오버플로 검사 컨텍스트를 제어합니다.

[!code-csharp-interactive[checked and unchecked](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#CheckedUnchecked)]

기본적으로 산술 연산은 *unchecked* 컨텍스트에서 발생합니다.

### <a name="floating-point-arithmetic-overflow"></a>부동 소수점 산술 오버플로

`float` 및 `double` 형식을 포함한 산술 연산은 예외를 throw하지 않습니다. 이러한 형식의 산술 연산 결과는 무한대를 나타내거나 숫자가 아닌 특수 값 중 하나일 수 있습니다.

[!code-csharp-interactive[double non-finite values](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#FloatingPointOverflow)]

`decimal` 형식의 피연산자의 경우 산술 오버플로는 항상 <xref:System.OverflowException>을 throw하고, 0으로 나누기는 항상 <xref:System.DivideByZeroException>을 throw합니다.

## <a name="round-off-errors"></a>반올림 오류

실수 및 부동 소수점 산술의 부동 소수점 표현을 일반적으로 제한함으로 인해 부동 소수점 형식을 사용하는 계산에서 반올림 오류가 발생할 수 있습니다. 즉, 생성된 식의 결과는 예상되는 수학적 결과와 다를 수 있습니다. 다음 예제에서는 이러한 몇몇 사례에 대해 설명합니다.

[!code-csharp-interactive[round-off errors](~/samples/csharp/language-reference/operators/ArithmeticOperators.cs#RoundOffErrors)]

자세한 내용은 [System.Double](/dotnet/api/system.double#remarks), [System.Single](/dotnet/api/system.single#remarks) 또는 [System.Decimal](/dotnet/api/system.decimal#remarks) 참조 페이지에서 설명을 참조하세요.

## <a name="operator-overloadability"></a>연산자 오버로드 가능성

사용자 정의 형식은 단항(`++`, `--`, `+` 및 `-`) 및 이진(`*`, `/`, `%`, `+` 및 `-`) 산술 연산자를 [오버로드](operator-overloading.md)할 수 있습니다. 이항 연산자가 오버로드되면 해당하는 복합 대입 연산자도 암시적으로 오버로드됩니다. 사용자 정의 형식은 복합 대입 연산자를 명시적으로 오버로드할 수 없습니다.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 다음 섹션을 참조하세요.

- [후위 증가 및 감소 연산자](~/_csharplang/spec/expressions.md#postfix-increment-and-decrement-operators)
- [전위 증가 및 감소 연산자](~/_csharplang/spec/expressions.md#prefix-increment-and-decrement-operators)
- [단항 더하기 연산자](~/_csharplang/spec/expressions.md#unary-plus-operator)
- [단항 빼기 연산자](~/_csharplang/spec/expressions.md#unary-minus-operator)
- [곱하기 연산자](~/_csharplang/spec/expressions.md#multiplication-operator)
- [나누기 연산자](~/_csharplang/spec/expressions.md#division-operator)
- [나머지 연산자](~/_csharplang/spec/expressions.md#remainder-operator)
- [더하기 연산자](~/_csharplang/spec/expressions.md#addition-operator)
- [빼기 연산자](~/_csharplang/spec/expressions.md#subtraction-operator)
- [복합 할당](~/_csharplang/spec/expressions.md#compound-assignment)
- [Checked 및 Unchecked 연산자](~/_csharplang/spec/expressions.md#the-checked-and-unchecked-operators)
- [숫자 승격](~/_csharplang/spec/expressions.md#numeric-promotions)

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 연산자](index.md)
- <xref:System.Math?displayProperty=nameWithType>
- <xref:System.MathF?displayProperty=nameWithType>
- [.NET의 숫자](../../../standard/numerics.md)
