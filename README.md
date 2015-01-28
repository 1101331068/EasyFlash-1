# EasyFlash ʹ��˵��

---

## 1������

EasyFlash��һ�Դ��������Ƕ��ʽFlash�洢���⣬��ҪΪMCU(Micro Control Unit)�ṩ��ݡ�ͨ�õ��ϲ�Ӧ�ýӿڣ�ʹ�ÿ����߸��Ӹ�Чʵ�ֻ��ڵ�Flash�洢������Ӧ�ÿ������ÿ�Ŀǰ�ṩ **����ʵ�ù���** ��

 - **Env** �ñ�����������ʵ�ֵ��籣�棬���赣�ı������ȡ����������
 
 ʹ�� **��ֵ��(key-value)** ��ʽ�������洢��Flash�У�����U-Boot�� `��������` ��ʹ�÷�ʽ��U-Bootһ�¡�
 - **IAP** ����������Ҳ�������¶�
 
 �ÿ��װ��IAP(In-Application Programming)���ܳ��õĽӿڣ�֧��CRC32У�飬ͬʱ֧��Bootloader��Application��������

### 1.1���ļ��ṹ

|Դ�ļ�                                 |����   |
|:------------------------------        |:----- |
|\flash\src\flash_env.c                 |Env��������������ز����ӿڼ�ʵ��Դ��|
|\flash\src\flash_iap.c                 |IAP��������������ز����ӿڼ�ʵ��Դ��|
|\flash\src\flash_utils.c               |EasyFlash����С���ߣ����磺CRC32|
|\flash\src\flash.c                     |Ŀǰֻ����EasyFlash��ʼ������|
|\flash\port\flash_port.c               |��ͬƽ̨�µ�EasyFlash��ֲ�ӿڼ����ò���|
|\demo\stm32f10x                        |stm32f10xƽ̨�µ�demo|

### 1.2����Դռ��

```
���Ҫ�� ROM: 6K bytes     RAM: 0.5K bytes + (Env��С)

Demoƽ̨��STM32F103RET6 + RT-Thread 1.2.2 + Env(2K bytes)
ʵ��ռ�ã� ROM: 6K bytes     RAM: 2.6K bytes
```

### 1.3��֧��ƽ̨

Ŀǰ����ֲƽֻ̨�� `STM32F10X` ϵ�е�Ƭ��Flash�����Ҳ�Ǳ��߲�Ʒʹ�õ�ƽ̨������ƽ̨����ֲ�ѶȲ�������Ŀ�����֮�����п����������ƽ̨�����������⣨64λ���⣩�����Զ�������ֲ�ӿڶ�����Ԥ������ֲֻ���޸� `\flash\port\flash_port.c` һ���ļ���ʵ������Ĳ���д��������ӡ���ܼ��ɡ�

��ӭ��� **fork and pull request** ����Դ����ĳɹ��벻�������˵�Ŭ����Ҳϣ������Ŀ�ܹ�������ҽ��Ϳ������ڣ��ò�Ʒ����Ļ�óɹ���

## 2������

### 2.1����������

��ͼΪ�˹�ͨ������̨�����û��������ĳ��ýӿڣ���ʾ�˻������� `"temp"` �Ӵ��������棬���޸ģ����ɾ���Ĺ��̡���Щ�ӿڶ�֧�ֱ�Ӧ�ò�ֱ�ӵ��á�

![easy_flash_env](https://cloud.githubusercontent.com/assets/1734686/5886463/46ad7efa-a3db-11e4-8401-75c00a4c35ba.gif)

### 2.2����������

��ͼ��ʾ��ͨ������̨������IAP��������Ĺ��̣�ʹ�õ��ǿ����Դ���IAP���ܽӿڣ���ʾ���õ��Ǵ���+YmodemЭ��ķ�ʽ���㻹Ҳ����ʵ��ͨ��CAN��485����̫�������ߣ���ʵ��Զ��������¡�

![easy_flash_iap](https://cloud.githubusercontent.com/assets/1734686/5886462/40f7d62c-a3db-11e4-866a-ba827c809370.gif)

## 3��API

����֧�ֵ�API�ӿڶ��� `\flash\inc\flash.h` ���������������ݽ϶࣬����ʹ�� **CTRL+F** ������

���ʽ��ܣ�
**������** ����EasyFlash�����һ����Ż��������������س����Flash������ϸ�洢�ܹ����Բο� `\flash\src\flash.c` �ļ�ͷλ�õ�ע��˵����
**����������** �����������еĻ����������ñ���Flash��RAM�о����ڣ��ϵ�����Flash���ص�RAM�У��޸ĺ�����Ҫ��������Flash�С�

### 3.1 ��ʼ��

��ʼ��EasyFlash���ڳ�ʼ���Ĺ����л�ʹ�� `\flash\port\flash_port.c` �е��û��Զ��������

```C
FlashErrCode flash_init(void)
```


### 3.2 ��������

#### 3.2.1 ���ػ�������

����Flash�е����л���������ϵͳ�ڴ��С�

```C
void flash_load_env(void)
```

#### 3.2.2 ��ӡ��������

ͨ������ֲ�ӿ�( `\flash\port\flash_port.c` )�ж���� `flash_print` ��ӡ����������Flash�е����л����������������

```C
void flash_print_env(void)
```

#### 3.2.3 ��ȡ��������

ͨ��������������������ȡ���Ӧ��ֵ����ע�⣺�˴��Ļ�������ָ�����Ѽ��ص��ڴ��еĻ���������

```C
char *flash_get_env(const char *key)
```

|����                                    |����|
|:-----                                  |:----|
|key                                     |������������|

#### 3.2.4 ���û�������

ʹ�ô˷�������ʵ�ֶԻ������������ӡ��޸ļ�ɾ�����ܡ���ע�⣺�˴��Ļ�������ָ�����Ѽ��ص��ڴ��еĻ���������
**����** ���������������в����ڸ����ƵĻ�������ʱ�����ִ������������
**�޸�** ������еĻ������������ڵ�ǰ�����������д��ڣ���Ѹû�������ֵ�޸�Ϊ����е�ֵ��
**ɾ��** ��������е�valueΪ��ʱ�����ɾ���������Ӧ�Ļ���������

```C
FlashErrCode flash_set_env(const char *key, const char *value)
```

|����                                    |����|
|:-----                                  |:----|
|key                                     |������������|
|value                                   |��������ֵ|

#### 3.2.5 ���滷������

�����ڴ��еĻ���������Flash�С�

```C
FlashErrCode flash_save_env(void)
```

#### 3.2.6 �ָ���������
���ڴ��еĻ���������ָ�ΪĬ��ֵ��

```C
FlashErrCode flash_env_set_default(void)
```

#### 3.2.7 ��ȡ��������������������

```C
uint32_t flash_get_env_total_size(void)
```

#### 3.2.8 ��ȡ��ǰ��ʹ�û��������Ĵ�С

```C
uint32_t flash_get_env_used_size(void)
```

### 3.3 ��������

#### 3.3.1 �����������е�Ӧ�ó���

```C
FlashErrCode flash_erase_bak_app(size_t app_size)
```

#### 3.3.2 �����û���Ӧ�ó���

ע�⣺�벻Ҫ��Ӧ�ó����е��ø÷���

```C
FlashErrCode flash_erase_user_app(uint32_t user_app_addr, size_t user_app_size)
```

|����                                    |����|
|:-----                                  |:----|
|user_app_addr                           |�û�Ӧ�ó�����ڵ�ַ|
|user_app_size                           |�û�Ӧ�ó����С|

#### 3.3.3 ����Bootloader

ע�⣺�벻Ҫ��Bootloader�е��ø÷���

```C
FlashErrCode flash_erase_bl(uint32_t bl_addr, size_t bl_size)
```

|����                                    |����|
|:-----                                  |:----|
|bl_addr                                 |Bootloader��ڵ�ַ|
|bl_size                                 |Bootloader��С|

#### 3.3.4 д���ݵ�������

Ϊ���س��򵽱��������Ƶ�Flash����д������
ע�⣺д֮ǰ����ȷ��Flash�ѽ��в�����

```C
FlashErrCode flash_write_data_to_bak(uint8_t *data,
                                     size_t size,
                                     size_t *cur_size,
                                     size_t total_size)
```

|����                                    |����|
|:-----                                  |:----|
|data                                    |��Ҫд�뵽�������е����ݴ洢��ַ|
|size                                    |�˴�д�����ݵĴ�С���ֽڣ�|
|cur_size                                |֮ǰ��д�뵽�������е����ݴ�С���ֽڣ�|
|total_size                              |��Ҫд�뵽�������������ܴ�С���ֽڣ�|

#### 3.3.5 �ӱ��ݿ���Ӧ�ó���

�������������غõ�Ӧ�ó��򿽱����û�Ӧ�ó�����ʼ��ַ��
ע�⣺
1������ǰ�����ԭ�е�Ӧ�ó�����в���
2����Ҫ��Ӧ�ó����е��ø÷���

```C
FlashErrCode flash_copy_app_from_bak(uint32_t user_app_addr, size_t app_size)
```

|����                                    |����|
|:-----                                  |:----|
|user_app_addr                           |�û�Ӧ�ó�����ڵ�ַ|
|user_app_size                           |�û�Ӧ�ó����С|

#### 3.3.5 �ӱ��ݿ���Bootloader

�������������غõ�Bootloader������Bootloader��ʼ��ַ��
ע�⣺
1������ǰ�����ԭ�е�Bootloader���в���
2����Ҫ��Bootloader�е��ø÷���

```C
FlashErrCode flash_copy_bl_from_bak(uint32_t bl_addr, size_t bl_size)
```

|����                                    |����|
|:-----                                  |:----|
|bl_addr                                 |Bootloader��ڵ�ַ|
|bl_size                                 |Bootloader��С|

### 3.4 ��ֲ


#### 3.4.1 ��ȡFlash

��С��λΪ4���ֽ�

```C
FlashErrCode flash_read(uint32_t addr, uint32_t *buf, size_t size)
```

|����                                    |����|
|:-----                                  |:----|
|addr                                    |��ȡ��ʼ��ַ|
|buf                                     |��Ŷ�ȡ���ݵĻ�����|
|size                                    |��ȡ���ݵĴ�С���ֽڣ�|

#### 3.4.2 ����Flash

```C
FlashErrCode flash_erase(uint32_t addr, size_t size)
```

|����                                    |����|
|:-----                                  |:----|
|addr                                    |������ʼ��ַ|
|size                                    |�������ݵĴ�С���ֽڣ�|

#### 3.4.3 д��Flash

��С��λΪ4���ֽ�

```C
FlashErrCode flash_write(uint32_t addr, const uint32_t *buf, size_t size)
```

|����                                    |����|
|:-----                                  |:----|
|addr                                    |д�����ʼ��ַ|
|buf                                     |Դ���ݵĻ�����|
|size                                    |д�����ݵĴ�С���ֽڣ�|

#### 3.4.4 ���䶯̬�ڴ�

```C
void *flash_malloc(size_t size)
```

|����                                    |����|
|:-----                                  |:----|
|size                                    |�������ڴ��С|

#### 3.4.5 �ͷŶ�̬�ڴ�

```C
void flash_free(void *p)
```

|����                                    |����|
|:-----                                  |:----|
|p                                       |���ͷŵĶ�̬�ڴ��ַ|

#### 3.4.6 ��ӡ������־��Ϣ

�ڶ��� `FLASH_PRINT_DEBUG` ��󣬴�ӡ������־��Ϣ

```C
void flash_log_debug(const char *file, const long line, const char *format, ...)
```

|����                                    |����|
|:-----                                  |:----|
|file                                    |���ø÷������ļ�|
|line                                    |���ø÷������к�|
|format                                  |��ӡ��ʽ|
|...                                     |������|

#### 3.4.7 ��ӡ��ͨ��־��Ϣ

```C
void flash_log_info(const char *format, ...)
```

|����                                    |����|
|:-----                                  |:----|
|format                                  |��ӡ��ʽ|
|...                                     |������|

#### 3.4.8 �޸�ʽ��ӡ��Ϣ

�÷�������޹̶���ʽ�Ĵ�ӡ��Ϣ��Ϊ `flash_print_env` �������á��� `flash_log_debug` �� `flash_log_info` ���������ָ��ǰ׺����ʽ�Ĵ�ӡ��־��Ϣ��

```C
void flash_print(const char *format, ...)
```

|����                                    |����|
|:-----                                  |:----|
|format                                  |��ӡ��ʽ|
|...                                     |������|

## 4��ע��

1��д����ǰ��ؼǵ��Ȳ�����
2�����������������ֻ�е��� `flash_save_env` �Żᱣ����Flash�У����򿪻��ᶪʧ�޸ĵ����ݣ�
3����Ҫ��Ӧ�ó���Bootloader��ִ�в�������������Ķ�����
4��Flash��ȡ��д�뷽������С��λΪ4���ֽڣ���������С��λ��������û���ƽ̨��ȷ����


