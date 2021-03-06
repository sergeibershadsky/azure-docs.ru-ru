## <a name="incremental-and-complete-deployments"></a>Добавочные и полные развертывания
При развертывании имеющихся ресурсов можно указать, что развертывание является добавочным или полным обновлением. Основное различие между этими двумя режимами заключается в том, как Resource Manager обрабатывает имеющиеся ресурсы в группе ресурсов, которых нет в шаблоне.

* При использовании полного режима Resource Manager **удаляет** ресурсы, которые существуют в группе ресурсов, но не указаны в шаблоне. 
* В инкрементном режиме Resource Manager **оставляет без изменения** ресурсы, которые существуют в группе ресурсов, но не указаны в шаблоне.

Для обоих режимов Resource Manager пытается подготовить все ресурсы, указанные в шаблоне. Если ресурс уже существует в группе ресурсов и его параметры не изменились, результаты операции останутся прежними. Если параметры ресурса были изменены, ресурс будет использовать новые параметры. При попытке обновить расположение или тип имеющегося ресурса развертывание завершится ошибкой. Вместо этого вы можете развернуть новый ресурс нужного вам типа с необходимым расположением.

По умолчанию Resource Manager использует инкрементный режим.

Чтобы понять различие между инкрементным и полным режимом, рассмотрим следующий сценарий.

**Имеющаяся группа ресурсов** содержит:

* ресурс А;
* ресурс Б;
* ресурс В.

**Шаблон** определяет:

* ресурс А;
* ресурс Б;
* ресурс Г.

При развертывании в **инкрементном** режиме группа ресурсов содержит:

* ресурс А;
* ресурс Б;
* ресурс В;
* ресурс Г.

При развертывании в **полном** режиме ресурс В будет удален. Группа ресурсов содержит:

* ресурс А;
* ресурс Б;
* ресурс Г.
