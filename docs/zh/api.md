# EasyFlash API ˵��

---

����֧�ֵ�API�ӿڶ��� `\flash\inc\flash.h` ���������������ݽ϶࣬����ʹ�� **CTRL+F** ������

���ʽ��ܣ�

**������** ����EasyFlash�����һ����Ż��������������س����Flash������ϸ�洢�ܹ����Բο� `\flash\src\flash.c` �ļ�ͷλ�õ�ע��˵����

**����������** �����������еĻ����������ñ���Flash��RAM�о����ڣ��ϵ�����Flash���ص�RAM�У��޸ĺ�����Ҫ��������Flash�С���

## 1���û�ʹ�ýӿ�

### 1.1 ��ʼ��

��ʼ��EasyFlash���ڳ�ʼ���Ĺ����л�ʹ�� `\flash\port\flash_port.c` �е��û��Զ��������

```C
FlashErrCode flash_init(void)
```

### 1.2 ��������

#### 1.2.1 ���ػ�������

����Flash�е����л���������ϵͳ�ڴ��С�

```C
void flash_load_env(void)
```

#### 1.2.2 ��ӡ��������

ͨ������ֲ�ӿ�( `\flash\port\flash_port.c` )�ж���� `flash_print` ��ӡ����������Flash�е����л����������������

```C
void flash_print_env(void)
```

#### 1.2.3 ��ȡ��������

ͨ��������������������ȡ���Ӧ��ֵ����ע�⣺�˴��Ļ�������ָ�����Ѽ��ص��ڴ��еĻ���������

```C
char *flash_get_env(const char *key)
```

|����                                    |����|
|:-----                                  |:----|
|key                                     |������������|

#### 1.2.4 ���û�������

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

#### 1.2.5 ���滷������

�����ڴ��еĻ���������Flash�С�

```C
FlashErrCode flash_save_env(void)
```

#### 1.2.6 �ָ���������
���ڴ��еĻ���������ָ�ΪĬ��ֵ��

```C
FlashErrCode flash_env_set_default(void)
```

#### 1.2.7 ��ȡ��������������������

```C
uint32_t flash_get_env_total_size(void)
```

#### 1.2.8 ��ȡ��ǰ��ʹ�û��������Ĵ�С

```C
uint32_t flash_get_env_used_size(void)
```

### 1.3 ��������

#### 1.3.1 �����������е�Ӧ�ó���

```C
FlashErrCode flash_erase_bak_app(size_t app_size)
```

#### 1.3.2 �����û���Ӧ�ó���

ע�⣺�벻Ҫ��Ӧ�ó����е��ø÷���

```C
FlashErrCode flash_erase_user_app(uint32_t user_app_addr, size_t user_app_size)
```

|����                                    |����|
|:-----                                  |:----|
|user_app_addr                           |�û�Ӧ�ó�����ڵ�ַ|
|user_app_size                           |�û�Ӧ�ó����С|

#### 1.3.3 ����Bootloader

ע�⣺�벻Ҫ��Bootloader�е��ø÷���

```C
FlashErrCode flash_erase_bl(uint32_t bl_addr, size_t bl_size)
```

|����                                    |����|
|:-----                                  |:----|
|bl_addr                                 |Bootloader��ڵ�ַ|
|bl_size                                 |Bootloader��С|

#### 1.3.4 д���ݵ�������

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

#### 1.3.5 �ӱ��ݿ���Ӧ�ó���

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

#### 1.3.5 �ӱ��ݿ���Bootloader

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

## 2 ��ֲ�ӿ�

### 2.1 ��ȡFlash

��С��λΪ4���ֽ�

```C
FlashErrCode flash_read(uint32_t addr, uint32_t *buf, size_t size)
```

|����                                    |����|
|:-----                                  |:----|
|addr                                    |��ȡ��ʼ��ַ|
|buf                                     |��Ŷ�ȡ���ݵĻ�����|
|size                                    |��ȡ���ݵĴ�С���ֽڣ�|

### 2.2 ����Flash

```C
FlashErrCode flash_erase(uint32_t addr, size_t size)
```

|����                                    |����|
|:-----                                  |:----|
|addr                                    |������ʼ��ַ|
|size                                    |�������ݵĴ�С���ֽڣ�|

### 2.3 д��Flash

��С��λΪ4���ֽ�

```C
FlashErrCode flash_write(uint32_t addr, const uint32_t *buf, size_t size)
```

|����                                    |����|
|:-----                                  |:----|
|addr                                    |д�����ʼ��ַ|
|buf                                     |Դ���ݵĻ�����|
|size                                    |д�����ݵĴ�С���ֽڣ�|

### 2.4 ���䶯̬�ڴ�

```C
void *flash_malloc(size_t size)
```

|����                                    |����|
|:-----                                  |:----|
|size                                    |�������ڴ��С|

### 2.5 �ͷŶ�̬�ڴ�

```C
void flash_free(void *p)
```

|����                                    |����|
|:-----                                  |:----|
|p                                       |���ͷŵĶ�̬�ڴ��ַ|

### 2.6 ��ӡ������־��Ϣ

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

### 2.7 ��ӡ��ͨ��־��Ϣ

```C
void flash_log_info(const char *format, ...)
```

|����                                    |����|
|:-----                                  |:----|
|format                                  |��ӡ��ʽ|
|...                                     |������|

### 2.8 �޸�ʽ��ӡ��Ϣ

�÷�������޹̶���ʽ�Ĵ�ӡ��Ϣ��Ϊ `flash_print_env` �������á��� `flash_log_debug` �� `flash_log_info` ���������ָ��ǰ׺����ʽ�Ĵ�ӡ��־��Ϣ��

```C
void flash_print(const char *format, ...)
```

|����                                    |����|
|:-----                                  |:----|
|format                                  |��ӡ��ʽ|
|...                                     |������|

## 3������

���øÿ���Ҫ��`\flash\flash.h`�ļ����������رն�Ӧ�ĺ꼴�ɡ�

### 3.1 CRC32У��

- Ĭ��״̬������
- �����������������ر�`FLASH_ENV_USING_CRC_CHECK`�꼴��

### 3.2 ĥ��ƽ��/���� ģʽ

- Ĭ��״̬������ģʽ
- ĥ��ƽ��ģʽ����`FLASH_ENV_USING_WEAR_LEVELING_MODE`���ر�`FLASH_ENV_USING_NORMAL_MODE`
- ����ģʽ����`FLASH_ENV_USING_NORMAL_MODE`���ر�`FLASH_ENV_USING_WEAR_LEVELING_MODE`
- ע�⣺ֻ��ѡ������һ��ģʽ������ģʽ����ͬʱʹ��

## 4��ע��

- д����ǰ��ؼǵ��Ȳ���
- ���������������ֻ�е��� `flash_save_env`�Żᱣ����Flash�У����򿪻��ᶪʧ�޸ĵ�����
- ��Ҫ��Ӧ�ó���Bootloader��ִ�в�������������Ķ���
- Flash��ȡ��д�뷽������С��λΪ4���ֽڣ���������С��λ��������û���ƽ̨��ȷ��


