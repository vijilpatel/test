# test


public static DateTime ConvertToLocal(DateTime dateTime)
		{
			DateTime result;
			try
			{
				switch (dateTime.Kind)
				{
				case DateTimeKind.Unspecified:
					result = DateTime.SpecifyKind(dateTime, DateTimeKind.Local);
					break;
				case DateTimeKind.Utc:
					result = dateTime.ToLocalTime();
					break;
				default:
					result = dateTime;
					break;
				}
			}
			catch (Exception ex)
			{
				throw ex;
			}
			return result;
		}

		public static DateTime? ConvertToLocal(DateTime? dateTime)
		{
			DateTime? result = null;
			try
			{
				if (dateTime.HasValue)
				{
					switch (dateTime.Value.Kind)
					{
					case DateTimeKind.Unspecified:
						result = new DateTime?(DateTime.SpecifyKind(dateTime.Value, DateTimeKind.Local));
						break;
					case DateTimeKind.Utc:
						result = new DateTime?(dateTime.Value.ToLocalTime());
						break;
					default:
						result = new DateTime?(dateTime.Value);
						break;
					}
				}
			}
			catch (Exception ex)
			{
				throw ex;
			}
			return result;
		}

		public static DateTime ConvertToUtc(DateTime dateTime)
		{
			DateTime result;
			try
			{
				switch (dateTime.Kind)
				{
				case DateTimeKind.Unspecified:
					result = DateTime.SpecifyKind(dateTime, DateTimeKind.Local);
					goto IL_32;
				case DateTimeKind.Local:
					result = dateTime.ToUniversalTime();
					goto IL_32;
				}
				result = dateTime;
				IL_32:;
			}
			catch (Exception ex)
			{
				throw ex;
			}
			return result;
		}

		public static DateTime? ConvertToUtc(DateTime? dateTime)
		{
			DateTime? result = null;
			try
			{
				if (dateTime.HasValue)
				{
					switch (dateTime.Value.Kind)
					{
					case DateTimeKind.Unspecified:
						result = new DateTime?(DateTime.SpecifyKind(dateTime.Value, DateTimeKind.Local));
						goto IL_6F;
					case DateTimeKind.Local:
						result = new DateTime?(dateTime.Value.ToUniversalTime());
						goto IL_6F;
					}
					result = new DateTime?(dateTime.Value);
				}
				IL_6F:;
			}
			catch (Exception ex)
			{
				throw ex;
			}
			return result;
		}

	public static DateTime ToDateTime(this object value)
		{
			if (value != null && value != DBNull.Value)
			{
				return DateTime.SpecifyKind(Convert.ToDateTime(value), DateTimeKind.Local);
			}
			return DateTime.Now;
		}

		public static DateTime ToDateTime(this string value)
		{
			if (!string.IsNullOrEmpty(value))
			{
				return DateTime.SpecifyKind(Convert.ToDateTime(value), DateTimeKind.Local);
			}
			return DateTime.Now;
		}
