# C�ṹ���� JSON ���ٻ�ת��

---

## struct2json

[struct2json](https://github.com/armink/struct2json) ��һ����Դ��C�ṹ���� JSON ���ٻ�ת�⣬�����Կ���ʵ�� **�ṹ�����** �� **JSON ����** ֮�����л��������л�Ҫ�󡣿��١����� API ��ƣ���󽵵�ֱ��ʹ�� JSON ��������ʵ�ִ��๦�ܵĴ��븴�Ӷȡ�

## ��Դ

������������Ӧ�õ�C�����У��ǵ��º����е����˼�롣����C������û���࣬����һ��ʹ�ýṹ�� `struct` �䵱�࣬��ô�ṹ��������Ƕ������˶���֮�󣬺ܶ�ʱ����Ҫ���Ƕ�������л��������л����⡣C���Բ���ܶ�߼�����ӵ�з���Ȼ��ƣ�ʹ�ö������л��������л���ԭ����֧�֡�

����C������˵�����л�Ϊ JSON �ַ����Ǹ������ѡ�����Ծ͵�ʹ�� [cJSON](https://github.com/kbranigan/cJSON) ���� JSON �����⣬����ʹ�ú�Ĵ����������߼��Բ����������cJSON����ж��η�װ��ʵ��һ�� struct �� JSON ֮����ٻ�ת�Ŀ⡣ struct2json �͵����ڴˡ������� struct2json ��Ҫʹ�ó�����

- **�־û�** ���ṹ��������л�Ϊ JSON ����󣬿�ֱ�ӱ������ļ���Flash��ʵ�ֶԽṹ�����ĵ���洢��
- **ͨ��** ���߼����Զ�JSON֧�ֵĺ��Ѻã����磺 Javascript��Groovy �Ͷ� JSON ����ԭ����֧�֣����� JSON Ҳ����ΪC�����������������֮���ͨ��Э���ʽ�����󴫵ݸ�ʽ��
- **���ӻ�** �����л�Ϊ JSON ��Ķ��󣬿��Ը���ֱ�۵�չʾ������̨���� UI �ϣ������ڲ�Ʒ���ԡ���Ʒ���ο����ȳ�����

## ���ʹ��

### �����ṹ��

���������������ṹ�壬�ṹ�� `Hometown` �ǽṹ�� `Student` ���ӽṹ��

```C
/* ���� */
typedef struct {
    char name[16];
} Hometown;

/* ѧ�� */
typedef struct {
    uint8_t id;
    uint8_t score[8];
    char name[10];
    double weight;
    Hometown hometown;
} Student;
```

### ���ṹ��������л�Ϊ JSON ����

|δʹ�ã�[Դ�ļ�](https://github.com/armink/struct2json/blob/master/docs/zh/assets/not_use_struct2json.c)��|ʹ�ú�[Դ�ļ�](https://github.com/armink/struct2json/blob/master/docs/zh/assets/used_struct2json.c)��|
|:-----:|:-----:|
|![�ṹ��תJSON-ʹ��ǰ](https://git.oschina.net/Armink/struct2json/raw/master/docs/zh/images/not_use_struct2json.png)| ![�ṹ��תJSON-ʹ�ú�](https://git.oschina.net/Armink/struct2json/raw/master/docs/zh/images/used_struct2json.png)|

### �� JSON �������л�Ϊ�ṹ�����

|δʹ�ã�[Դ�ļ�](https://github.com/armink/struct2json/blob/master/docs/zh/assets/not_use_struct2json_for_json.c)��|ʹ�ú�[Դ�ļ�](https://github.com/armink/struct2json/blob/master/docs/zh/assets/used_struct2json_for_json.c)��|
|:-----:|:-----:|
|![JSONת�ṹ��-ʹ��ǰ](https://git.oschina.net/Armink/struct2json/raw/master/docs/zh/images/not_use_struct2json_for_json.png)| ![JSONת�ṹ��-ʹ�ú�](https://git.oschina.net/Armink/struct2json/raw/master/docs/zh/images/used_struct2json_for_json.png)|

��ӭ��� **fork and pull request**([Github](https://github.com/armink/struct2json)|[OSChina](http://git.oschina.net/armink/struct2json)|[Coding](https://coding.net/u/armink/p/struct2json/git)) ��������������Դ��Ŀ���ޣ����Ե��[��Ŀ��ҳ](https://github.com/armink/struct2json) ���Ͻǵ�**Star**��ͬʱ�����Ƽ�����������Ҫ�����ѡ�

## �ĵ�

�������ݲο�[`\docs\zh\`](https://github.com/armink/struct2json/tree/master/docs/zh)�µ��ļ�����ر�֤�� **�Ķ��ĵ�** ����ʹ�á�

## ���

MIT Copyright (c) armink.ztl@gmail.com

```C
cJSON *struct_to_json(void* struct_obj) {
    Student *struct_student = (Student *)struct_obj;

    /* ����Student JSON���� */
    s2j_create_json_obj(json_student);

    /* ���л����ݵ�Student JSON���� */
    s2j_json_set_basic_element(json_student, struct_student, int, id);
    s2j_json_set_basic_element(json_student, struct_student, double, weight);
    s2j_json_set_array_element(json_student, struct_student, int, score, 8);
    s2j_json_set_basic_element(json_student, struct_student, string, name);

    /* ���л����ݵ�Student.Hometown JSON���� */
    s2j_json_set_struct_element(json_hometown, json_student, struct_hometown, struct_student, Hometown, hometown);
    s2j_json_set_basic_element(json_hometown, struct_hometown, string, name);

    /* ����Student JSON����ָ�� */
    return json_student;
}











```
```C
cJSON *struct_to_json(void* struct_obj) {
    Student *struct_student = (Student *) struct_obj;
    cJSON *score, *score_element;
    size_t index = 0;

    /* ����Student JSON���� */
    cJSON *json_student = cJSON_CreateObject();

    /* ���л����ݵ�Student JSON���� */
    cJSON_AddNumberToObject(json_student, "id", struct_student->id);
    cJSON_AddNumberToObject(json_student, "weight", struct_student->weight);
    score = cJSON_CreateArray();
    if (score) {
        while (index < 8) {
            score_element = cJSON_CreateNumber(struct_student->score[index++]);
            cJSON_AddItemToArray(score, score_element);
        }
        cJSON_AddItemToObject(json_student, "score", score);
    }
    cJSON_AddStringToObject(json_student, "name", struct_student->name);

    /* ���л����ݵ�Student.Hometown JSON���� */
    Hometown *hometown_struct = &(struct_student->hometown);
    cJSON *hometown_json = cJSON_CreateObject();
    cJSON_AddItemToObject(json_student, "hometown", hometown_json);
    cJSON_AddStringToObject(hometown_json, "name", hometown_struct->name);

    /* ����Student JSON����ָ�� */
    return json_student;
}

```


```C
void *json_to_struct(cJSON* json_obj) {
    /* ����Student�ṹ����� */
    s2j_create_struct_obj(struct_student, Student);

    /* �����л����ݵ�Student�ṹ����� */
    s2j_struct_get_basic_element(struct_student, json_obj, int, id);
    s2j_struct_get_array_element(struct_student, json_obj, int, score);
    s2j_struct_get_basic_element(struct_student, json_obj, string, name);
    s2j_struct_get_basic_element(struct_student, json_obj, double, weight);

    /* �����л����ݵ�Student.Hometown�ṹ����� */
    s2j_struct_get_struct_element(struct_hometown, struct_student, json_hometown, json_obj, Hometown, hometown);
    s2j_struct_get_basic_element(struct_hometown, json_hometown, string, name);

    /* ����Student�ṹ�����ָ�� */
    return struct_student;
}





























```

```
void *json_to_struct(cJSON* json_obj) {
    cJSON *json_temp, *score, *score_element;
    Student *struct_student;
    size_t index = 0, score_size = 0;

    /* ����Student�ṹ����� */
    struct_student = s2j_malloc(sizeof(Student));
    if (struct_student) {
        memset(struct_student, 0, sizeof(Student));
    }

    /* �����л����ݵ�Student�ṹ����� */
    json_temp = cJSON_GetObjectItem(json_obj, "id");
    if (json_temp) {
        struct_student->id = json_temp->valueint;
    }
    score = cJSON_GetObjectItem(json_obj, "score")
    if (score) {
        score_size = cJSON_GetArraySize(score);
        while (index < score_size) {
            score_element = cJSON_GetArrayItem(score, index);
            if (score_element) {
                struct_student->score[index++] = score_element->valueint;
            }
        }
    }
    json_temp = cJSON_GetObjectItem(json_obj, "name");
    if (json_temp) {
        strcpy(struct_student->name, json_temp->valuestring);
    }
    json_temp = cJSON_GetObjectItem(json_obj, "weight");
    if (json_temp) {
        struct_student->weight = json_temp->valuedouble;
    }

    /* �����л����ݵ�Student.Hometown�ṹ����� */
    Hometown *struct_hometown = &(struct_student->hometown);
    cJSON *json_hometown = cJSON_GetObjectItem(json_obj, "hometown");
    json_temp = cJSON_GetObjectItem(json_hometown, "name");
    if (json_temp) {
        strcpy(struct_hometown->name, json_temp->valuestring);
    }

    /* ����Student�ṹ�����ָ�� */
    return struct_student;
}
```