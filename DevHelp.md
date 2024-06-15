# Intro
Spoilers ahead. If you really want to build the code and don't want to struggle
through the datasheet, keep reading. 

## GPIO
### Initialization
```c
	// Initialize GPIOC Peripheral Clock (0x1 for bit 2 in RCC_AHB1ENR)
	RCC->AHB1ENR |= (1<<2);

	// Set port Input mode for PC2 (0x00 for bit 5 and 4 in GPIOC_MODER)
	GPIOC->MODER &= ~(0x00000030);

	// Set port Pull-upfor PC2 (0x01 for bit 5 and 4 in GPIOC_PUPDR)
	GPIOC->PUPDR |= 0x00000010;
```
### Checking Pins
```c
// PC3 can be checked by bit shifting a 1 to the correct register and checking the bit status
	if( ( GPIOC->IDR & ( 1 << 2 ) ) != 0 )
	{
		return 0;
	}
	else
	{
		return 1;
	}
```

## UART
### Initialize
```c
  huart1.Instance = USART1;
  huart1.Init.BaudRate = 115200;
  huart1.Init.WordLength = UART_WORDLENGTH_8B;
  huart1.Init.StopBits = UART_STOPBITS_1;
  huart1.Init.Parity = UART_PARITY_NONE;
  huart1.Init.Mode = UART_MODE_TX_RX;
  huart1.Init.HwFlowCtl = UART_HWCONTROL_NONE;
  huart1.Init.OverSampling = UART_OVERSAMPLING_16;
  if (HAL_UART_Init(&huart1) != HAL_OK)
  {
    Error_Handler();
  }
```
### Writing Data
```c
/* User should transmit the access granted string */
HAL_UART_Transmit(&huart1, (uint8_t*)accessGranted, strlen(accessGranted), 10 );

/* User should transmit the access denied string */
HAL_UART_Transmit(&huart1, (uint8_t*)accessDenied, strlen(accessDenied), 10 );

/* User should transmit the super user access granted string */
HAL_UART_Transmit(&huart1, (uint8_t*)superUserAccessGranted, strlen(superUserAccessGranted), 10 );

/* User should transmit the access denied string */
HAL_UART_Transmit(&huart1, (uint8_t*)accessDenied, strlen(accessDenied), 10 );
```
